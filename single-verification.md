# Single Verification

**Verify a sigle email address**

`POST /verify.json` will return the result of the verification of the submitted email address.

**Required parameters**: 
* `address` a the plain text body.

This endpoint will return `200 OK` with the verification JSON representation if the verification was a success.


###### Example JSON Response
    
    {
        "address": "nonexistentemail@example.com",
        "account": "nonexistentemail",
        "domain": "example.com",
        "md5": "f1fcb3c946953f6ef7602111a8efc4d4"
        "is_disposable_address": false,
        "is_role_address": false,
        "reason": [mailbox_does_not_exist],
        "result": "undeliverable",
        "risk": "high"
    }


###### Copy as cURL

    curl -H "Authorization: Bearer $ACCESS_TOKEN" \
        -H 'Content-Type: application/json' \
        -H 'User-Agent: MyApp (yourname@example.com)' \
        -d '{ "address": "nonexistentemail@example.com" }' \
        https://1.ghostbusterapi.com/$ACCOUNT_ID/verify.json
