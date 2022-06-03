# The Ghostbuster API

Welcome to the Ghostbuster API! If you're looking to integrate your application with [Ghostbuster.email](https://ghostbuster.email) you're in the right place. We're happy to have you!


## Making a request

All URLs start with `https://1.ghostbusterapi.com/999999999/`. URLs are HTTPS only. The path is prefixed with the account ID.

To make a request for verify an email, append the `verify` index path to the base URL to form something like `https://1.ghostbusterapi.com/999999999/verify.json`. In cURL, it looks like this:

    curl -H "Authorization: Bearer $ACCESS_TOKEN" -H 'User-Agent: MyApp (yourname@example.com)' https://1.ghostbusterapi.com/999999999/verify.json

Throughout the Ghostbuster API docs, we include "Copy as cURL" examples. To try the examples in your shell, copy your Access Token into your clipboard and run:

    export ACCESS_TOKEN=PASTE_ACCESS_TOKEN_HERE
    export ACCOUNT_ID=999999999

Then you should be able to copy/paste any example from the docs. After pasting a cURL example, you can pipe it to a JSON pretty printer to make it more readable. Try jsonpp or [json_pp](https://jmhodges.github.io/jsonpp/) on OSX:

    curl -s -H "Authorization: Bearer $ACCESS_TOKEN" https://1.ghostbusterapi.com/999999999/verify.json | json_pp

## Authentication

All API requests require authentication. To authenticate, you need an access token. You can find your access token by visiting your account [tokens section](https://app.ghostbuster.email/tokens).

Your Access Token must be sent as a [HTTP Authorization header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Authorization) in all requests, as shown below:

     Authorization: Bearer YOUR_ACCESS_TOKEN


## Identifying your application

You must include a User-Agent header with **both**:

* The name of your application
* A link to your application or your email address

We use this information to get in touch if you're doing something wrong (so we can warn you before you're blacklisted) or something awesome (so we can congratulate you). Here are examples of acceptable User-Agent headers:

* `User-Agent: Mailchimp (http://mailchimp.com/contact.php)`
* `User-Agent: Julia's Ingenious Integration (julia@example.com)`

If you don't include a `User-Agent` header, you'll get a `400 Bad Request` response.


