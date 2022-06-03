# Single Verification

**Verify a sigle email address**

`POST /verify.json` will return the result of the verification of the submitted email address.

**Required parameters**: 
* `address` a the plain text body.

This endpoint will return `200 OK` with the verification JSON representation if the verification was a success.

##### Copy as cURL

```bash
curl -H "Authorization: Bearer $ACCESS_TOKEN" \
    -H 'Content-Type: application/json' \
    -H 'User-Agent: MyApp (yourname@example.com)' \
    -d '{ "address": "nonexistentemail@example.com" }' \
    https://1.ghostbusterapi.com/$ACCOUNT_ID/verify.json
```

##### Example JSON Response

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

###### Field Explanation

| Parameter | Type | Description |
| :--- | :---: | :--- |
| address | string | E-mail address that has been verified. |
| account | string | The portion of the email address before the "@" symbol. |
| domain | string | The portion of the email address after the "@" symbol. |
| md5 | string | E-mail address that has been verified. |
| is_disposable_address | boolean | If the domain is in a list of disposable email addresses, this will be appropriately categorized. |
| is_role_address | boolean | Checks the mailbox portion of the email if it matches a specific role type (‘admin’, ‘sales’, ‘webmaster’). |
| reason | array | List of potential reasons why a specific verification may be unsuccessful. |
| result | string | Either `deliverable`, `undeliverable`, `do_not_send`, `catch_all` or `unknown`. Please see the [Result Types](#result-types) section below for details on each result type. |
| risk | string | `high`, `medium`, `low`, or `unknown` Depending on the evaluation of all aspects of the given email. |
| processed_at | string | The UTC time the email was validated.
| root_address | string | (Optional) If the address is an alias; this will contain the root email address with alias parts removed. |


###### Result Types
