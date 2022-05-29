# Getting Started

This step-by-step tutorial will have you running a successful email validation on Ghostbuster.email in minutes. Let's get started!

## About Ghostbuster.email

Ghostbuster.email is a cloud-based Email Verification service to achieve high deliverability rates.

Ghostbuster.email is built for productivity and guided by three principles:

* **Speed**: People work in a fast feedback loop, so API response must be fast.
* **Power**: Lead Email Verification should be able to be run from any automated software workflow, at any scale.
* **Ease of use**: Email verification should be easy enough for anyone to use, so that you can keep track of your customer growth and its impact on conversion rates.

Our verification service fits all your needs and has the highest detection rate of invalid, undeliverable and spam email addresses based on:

* Checking for correct syntax.
* Catch-all servers.
* Domain authentication.
* SMTP authentication. 

## Prerequisites

To complete this tutorial, you will need:

* Basic knowledge of API
* A [Ghostbuster.email](https://ghostbuster.email/register) account


## Creating a Ghostbuster.email account

* Got to the [Form registration](https://ghostbuster.email/register) in [Ghostbuster.email](https:://ghostbuster.email).
* Fill the **Create your new token** form with a token name and click the **Generate token** button.
* The **token will be generated** in the next step. Please **copy the new token**. For your security, it won't be shown again.


## Authentication
All API requests require authentication. To authenticate, you need an authentication token. You must to use the generated token in the previous step. Also, you are able to generate a new token by visiting your [API Tokens](https://gghostbuster.email/tokens) section.

Your Authentication Token must be sent as a HTTP header in all requests, as shown below:

    curl --request POST \
      --url https://api.ghostbuster.email/v1/verify \
      --header 'Authorization: Bearer {api_token}' \
      --header 'Content-Type: application/json' \
      --data '{
	        "email": "example@ghostbuster.email"
      }	'
      
## Errors

There are several errors that you can receive as a response to an API request.

**Failure to authenticate**

    HTTP/1.1 401 Unauthorized
    
**Requesting non-existing resources#**

    HTTP/1.1 404 Not Found


## Request

### Constraints

* All requests must use HTTPS.
* All data is sent and received as JSON.

### Running a verification

    POST api.ghostbuster.email/v1/verify
    
**Params**

* email (required) - email address to by verified

**Response**

    HTTP status: 200

    {
        "address": "example@ghostbuster.email",
        "account": "example",
        "domain": "ghostbuster.email",
        "md5Hash": "41d4f875da3bc665eb4276beeda3050f",
        "is_role_address": false,
        "result": "deliverable",
        "reason": "mailbox_exists",
        "code": 200
    }
    
**Example**

    curl --request POST \
      --url https://api.ghostbuster.email/v1/verify \
      --header 'Authorization: Bearer {api_token}' \
      --header 'Content-Type: application/json' \
      --data '{
	        "email": "example@ghostbuster.email"
      }	
