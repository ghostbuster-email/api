# Single Verification

Verify a sigle email address

## Endpoint

`POST /verify.json` will return the result of the verification of the submitted email address.

## Required parameters
* `address` a the plain text body.

## Copy as cURL

```bash
curl -H "Authorization: Bearer $ACCESS_TOKEN" \
    -H 'Content-Type: application/json' \
    -H 'User-Agent: MyApp (yourname@example.com)' \
    -d '{ "address": "nonexistentemail@example.com" }' \
    https://1.ghostbusterapi.com/$ACCOUNT_ID/verify.json
```

## Example Response

This endpoint will return `200 OK` with the verification JSON representation if the verification was a success.

```jsonl
{
    "address": "nonexistentemail@example.com",
    "account": "nonexistentemail",
    "domain": "example.com",
    "md5": "f1fcb3c946953f6ef7602111a8efc4d4"
    "is_disposable_address": false,
    "is_role_address": false,
    "reason": ["mailbox_does_not_exist"],
    "result": "undeliverable",
    "risk": "high"
}
```

### Field Explanation

| Parameter | Type | Description |
| :--- | :---: | :--- |
| address | string | E-mail address that has been verified. |
| account | string | The portion of the email address before the "@" symbol. |
| domain | string | The portion of the email address after the "@" symbol. |
| md5 | string | E-mail address that has been verified. |
| is_disposable_address | boolean | If the domain is in a list of disposable email addresses, this will be appropriately categorized. |
| is_role_address | boolean | Checks the mailbox portion of the email if it matches a specific role type (‘admin’, ‘sales’, ‘webmaster’). |
| reason | array | List of potential reasons why a specific verification may be unsuccessful. |
| result | string | Either `deliverable`, `undeliverable`, `do_not_send` or `unknown`. Please see the [Result Types](#result-types) section below for details on each result type. |
| risk | string | `high`, `medium`, `low`, or `unknown` Depending on the evaluation of all aspects of the given email. |
| root_address | string | (Optional) If the address is an alias; this will contain the root email address with alias parts removed. |


### Result Types

| Result | Description |
| :--- | :--- |
| deliverable | The recipient address is considered to be valid and should accept email. |
| undeliverable | The recipient address is considered to be invalid and will result in a bounce if sent to. |
| do_not_send | The recipient address is considered to be highly risky and will negatively impact sending reputation if sent to. |
| unknown | The validity of the recipient address cannot be determined for a variety of potential reasons. Typical cases are "Their mail server was down" or "the anti-spam system is blocking us". Remember **you are not charged for unknown results**, these requests will be deducted from your bill. If you still have a large number, contact us and we will take a look and verify.

### Reason Explanation

| Reason | Result| Description |
| :--- | :---: | :--- |
| immature_domain | deliverable | The domain is newly created based on the WHOIS information. |
| catch_all | deliverable | The validity of the recipient address cannot be determined as the provider accepts any and all email regardless of whether or not the recipient’s mailbox exists. |
| long_term_disposable | deliverable | The mailbox has been identified as a long term disposable address. Long term disposable addresses can be quickly and easily deactivated by users, but they will not expire without user intervention. |
| high_risk_domain | do_not_send | The domain has a top-level-domain (TLD) that has been identified as high risk. |
| mailbox_is_role_address | do_not_send | The mailbox is a role based address (ex. support@…, marketing@…). Role-based emails have a strong correlation to people reporting mails sent to them as spam and abuse.|
| mailbox_is_disposable_address | do_not_send | The mailbox has been identified to be a disposable address. Disposable address are temporary, generally one time use, addresses. |
| failed_syntax_check | undeliverable | Emails that fail RFC syntax protocols. |
| no_dns_entries | undeliverable |  These emails are valid in syntax, but the domain doesn't have any records in DNS or have incomplete DNS Records. Therefore, mail programs will be unable to or have difficulty sending to them. These emails are marked invalid.
| no_mx | undeliverable | The recipient domain does not have a valid MX host. |
| mailbox_not_found | undeliverable | The mailbox is undeliverable or does not exist. |
| mailbox_quota_exceeded | undeliverable | These emails exceeded their space quota and are not accepting emails. These emails are marked invalid. |
| mail_server_temporary_error | unknown | These emails belong to a mail server that is returning a temporary error. Most of the time, these emails will end up being invalid.|
| smtp_connection_error | unknown | These emails belong to a mail server that won't allow an SMTP connection. Most of the time, these emails will end up being invalid. |
| timeout_exceeded | unknown | These emails belong to a mail server that is responding extremely slow. Most of the time, these emails will end up being invalid.|
| exception_occurred | unknown | These emails caused an exception when validating. If this happens repeatedly, [please let us know](https://ghostbuster.email/support).



## Sandbox Mode

To help you test every scenario of results and reasons code with the API, we put together a list of emails that will return specific results when used with the API for testing purposes. **Testing with these emails will not be charged on your invoice.**

You will need to [authenticate](https://github.com/ghostbuster-email/api#authentication) with your ACCESS TOKEN in order to test with these email addresses.

- valid@example.com
- disposable@example.com
- undeliverable@example.com
- do_not_send@example.com
- unknown@example.com
- catch_all@example.com
- does_not_accept_mail@example.com
- failed_smtp_connection@example.com
- failed_syntax_check@example.com
- mail_server_temporary_error@example.com
- mailbox_quota_exceeded@example.com
- mailbox_not_found@example.com
- no_dns_entries@example.com
- role_based@example.com
- timeout_exceeded@example.com
