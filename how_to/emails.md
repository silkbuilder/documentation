# Emailing Process

The email functionality in SilkBuilder provides the tools to configure MIME wrappers and HTML email body templates. These are controlled by the system's **Email Schemas** option and the **Email Editor**, which is a project element.

Sending an email consists of inserting a row into the `silkEmailSent` table, which is part of the SilkBuilder framework database structure. An internal process periodically scans this table for new records and executes the email submission process.

> **Note:** The SilkBuilder email functionality is only available in the licensed version. It is not available in the free core version.

## Email Schemas

The system's **Email Schema** option is found after opening the "Options" folder in the project's structure panel. Once open, it lists and displays the default schema, `default.eml`.

This option allows you to edit the MIME structure that governs email generation. The editor provides tools to insert base64-encoded data or attachments, such as images, that can later be referenced in the HTML body.

The schema uses three basic placeholders to mark the relevant areas that are used when merging the schema with an email body during email generation and submission:

| Placeholder | Functionality |
| --------------- | ------------------------------------------------------------ |
| `{[subject]}` | Marks the place where the email's subject will be inserted in the schema. |
| `{[silkEmailTracker]}` | Inserts the **silkEmailTracker**, a unique email identifier inserted by the framework. |
| `{[message]}` | Marks the place where the email's body template will be inserted. |

> **Note:** The Email Schema requires the developer to have a basic understanding of MIME email structure. A misconfiguration can cascade into multiple errors for the receiving party.

## Email Templates

Email templates are elements added to a **Service Pool** element. A Service Pool can contain multiple email templates, each defining the email body to be used under a specific circumstance.

Each email template is assigned a unique **ID** (UUID), used to identify it during the email insert process.

The email template editor lets you edit the *Wrapper*, which is the file name of the previously defined email schema. If the specified file does not exist, the email submission process will fail.

The email body can be configured to support the multiple languages set up for the system. Each language's email body is independent and must be configured individually, including its attachment links.

The email body uses an HTML editor to provide rich content capabilities. The body is wrapped by the selected email schema during email generation.

### Dynamic Variables

Email templates support inserting variables, which act as data placeholders. Data supplied during the email creation (insert) process replaces these variables. Variables follow the format `${variable-name}` and can be placed in both the subject and the body.

A subject example:

```
Welcome to the ${event-name} event!
```

A body example:

```
Dear ${full-name},
We are happy to have you at the ${event-name} event!
```

### Attachments

Attachments can be added to an email template using the **Attachment Links** option. While in editing mode, click the [+] icon on the right side of the Attachment Links option. A pop-up window will ask for an identifier (name) and the storage path of the attachment file. When the email is created, the file is added to the email's MIME structure as a Base64-encoded attachment.

Examples:

Identifier: `privacy-notice`
Path: `/opt/docs/privacy-notice.pdf`

Identifier: `smiley-face`
Path: `/opt/images/smiley-face.jpg`

The attachment path supports the insertion of variables:

Identifier: `product-thumb`
Path: `/opt/images/products/${product-id}.jpg`

Multiple attachments can be added to a single email template.

### Attached Images in the Body

To display an attached image in the email body, use the attachment identifier as the image's URL, adding the `cid:` prefix to indicate that it should be loaded locally. For example:

Image path: `cid:product-thumb`

## Email Submission

Sending an email consists of executing an INSERT into the `silkEmailSent` table. The columns available for the insert are as follows:

| Column | Condition | Description |
| ------ | ------- | ----------- |
| emailUUID | **Required** | The email template's ID. |
| langID | Optional | The template language code to use. If not provided, English (en) is used by default. |
| actionTitle | **Required** | A description of the purpose of the email. |
| sentFrom | Optional | The "From" email address. If not provided, it is taken from the email template. If the template does not have one, the email address from the email server configuration is used. |
| replyTo | Optional | If not specified, it is taken from the email template. If the email template lacks it, it is not used. |
| sentTo | **Required** | The target email address. |
| copyTo | Optional | If not specified, it is taken from the email template. If the email template lacks it, it is not used. |
| blindTo | Optional | If not specified, it is taken from the email template. If the email template lacks it, it is not used. |
| variables | **Required** | The variable values that will fill the email template placeholders. |
| priority | Optional | The default value is "0." If it is changed to 1, the records will be positioned at the top of the list to give them priority during the row scanning process. |

### Variables Format

The `variables` column in the `silkEmailSent` table receives text formatted according to the pattern `variable_name=value`. Multiple variables follow the same pattern, separated by the `<|>` mark:

```
variable1=value1<|>variable2=value2<|>variable3=value3
```

This pattern is typically created using SQL string concatenation, with the values usually coming from the columns of a SELECT statement.

Example of variable pattern generation in MySQL, SQL Server, and PostgreSQL:

```
concat(
	'variable1=', value1, '<|>',
	'variable2=', value2, '<|>',
	'variable3=', value3
) as variables
```

Oracle uses this format:

```
'variable1=' || value1 || '<|>' ||
'variable2=' || value2 || '<|>' ||
'variable3=' || value3 as variables
```

### The Insert

Submitting an email consists of using the INSERT command to add one or more rows to the `silkEmailSent` table, which is periodically monitored for new records.

The best practice is to generate the email columns using a SELECT statement and use it to insert a row into the `silkEmailSent` table.

```sql
-- MySQL example
insert into silkEmailSent (
  emailUUID,
  actionTitle,
  sentTo,
  variables
)
select
	'79ca5c97-b5bd-4bc1-900f-a6d1036f89c0' as emailUUID, -- Email template ID
	'User Registration' as actionTitle,
	pr.emailAddress as sentTo,
	concat(
		'fullName=', pr.firstName, ' ', pr.lastName, '<|>',
		'categoryName=', ct.categoryName, '<|>',
    'registrationDate=', date_format(pr.creationDate,'%Y-%m-%d')
  ) as variables
from person pr
join category ct on pr.categoryID = ct.categoryID
where pr.personID = $P{personID}
```

The SELECT command can return multiple rows if the email is targeting multiple people.

The values used in the `silkEmailSent` insert can also be generated by a stored procedure and then passed directly into the INSERT command.

An internal process scans the `silkEmailSent` table for new records. When a new record is found, the process loads the schema (`default.eml`), uses the `emailUUID` to load the corresponding email template, replaces the variables with the provided values, and then sends the email to the SMTP server. 

## Email Processing Behavior

The internal process that dispatches emails follows a polling model with the following behavior:

**Polling and throttling**

The process runs in a loop at a configurable interval and can be configured to submit a limited number of rows per cycle. This prevents overwhelming the SMTP server when a large number of rows are inserted at once.

Rows that are not picked up in a given cycle (because the batch limit was reached) are not skipped or lost — they remain pending and are picked up in a subsequent cycle. Rows are processed in the order they were inserted, so no row is starved indefinitely by newer rows, except if the priority column is set to "1".

**Idempotency**

A row is only marked as submitted after it has been successfully handed off to the SMTP server. This prevents duplicate sends if the process is restarted or a cycle is interrupted, since already-submitted rows are excluded from future polling cycles.

**Error handling**

If an error occurs while processing a row (for example, an invalid `emailUUID`, a missing wrapper file, or an SMTP failure), the row is marked as **undeliverable** instead of submitted. Undeliverable rows are not automatically retried, so they should be periodically reviewed to identify and correct the underlying issue (e.g. bad data, misconfiguration, or a temporary mail server outage).

**Variable parsing**

When parsing the `variables` column, the process matches each variable name to the value using the *first* `=` symbol that follows it. Any additional `=` symbols within the value are treated as part of the value, not as delimiters. Because the `<|>`sequence is used to separate variable pairs, it should be avoided within variable values, as it cannot be distinguished from the actual field separator during parsing.

# Local Testing

To test the email process locally, you can install and configure **MailHog**. MailHog is a lightweight, open-source email-testing tool for developers. It runs a local, fake SMTP server that intercepts outgoing application emails and stores them in memory. You can download it using the instructions on the [MailHog GitHub page](https://github.com/mailhog/MailHog).

Using the SilkClient Setup page, configure the Mail service with this data:

| Property        | Value     |
| --------------- | --------- |
| Server Hostname | 127.0.0.1 |
| Port            | 1025      |
| Authentication  | Off       |
| Security        | No        |
| Context Path    | 127.0.0.1 |

This change requires a Tomcat restart.

To access the MailHog Email Client, go to: http://127.0.0.1:8025