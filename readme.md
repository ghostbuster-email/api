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


## JSON only

We use JSON for all API data. The style is no root element and snake_case for object keys. All API URLs end in `.json` to indicate that they return JSON. Alternatively you can send `Accept: application/json`.


## Handling errors

API clients must expect and gracefully handle transient errors, such as rate limiting or server errors. We recommend baking 5xx and 429 response handling into your low-level HTTP client so your integration can handle most errors automatically.

### Rate limiting (429 Too Many Requests)

You can perform up to 50 requests per 10-second period from the same IP address. If you exceed this limit, you'll get a [429 Too Many Requests](http://tools.ietf.org/html/draft-nottingham-http-new-status-02#section-4) response for subsequent requests. Check the `Retry-After` header to see how many seconds to wait before retrying the request.

### [5xx server errors](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#5xx_Server_errors)

If Ghostbuster is having trouble, you will get a response with a 5xx status code indicating a server error. 500 (Internal Server Error), 502 (Bad Gateway), 503 (Service Unavailable), and 504 (Gateway Timeout) may be retried with [exponential backoff](https://en.wikipedia.org/wiki/Exponential_backoff).

## API endpoints

* [Single Verification](https://github.com/ghostbuster-email/docs/blob/main/single-verification.md)
* [Bulk Verification](https://github.com/ghostbuster-email/docs/blob/main/bulk-verification.md)


## Conduct

Please note that this project is released with a Contributor Code of Conduct. By participating in discussions about the Ghostbuster API, you agree to abide by these terms.


## License

These API docs are licensed under Creative Commons (CC BY-SA 4.0). Please share, remix, and distribute as you see fit.

---

If you have a specific feature request or find a bug, [please open a GitHub issue](https://github.com/ghostbuster/api/issues/new). We encourage you to fork these docs for local reference and happily accept pull requests with improvements.

To talk with us and other developers about the API, [post a question on StackOverflow](http://stackoverflow.com/questions/ask) tagged `ghostbuster_email`. If you need help from us directly, [please open a support ticket](https://ghostbuster.email/support).
