# ServiceHub REST API

Digital Space ServiceHub REST API allows for you to make HTTP POST/GET/PUT/DELETE requests to specific endpoints that we have developed in order to create, manage and delete parts of the ServiceHub package from your own integration rather than the ServiceHub Web Portal.

_**Please note that all API calls will be made as a 'super user' - which basically means an admin level user is created on behalf of your company and linked to your API Key(s). When any API call is made, fields such as 'Created By', 'Requested By' and 'Updated By' will be pre-populated with your API Key's user rather than a specific user from your company. A future update will bring functionality to allow these to be provided within a request object (so that specific user's within your company can be assigned to an Incident for example).**_

## Requirements

* Must be a Digital Space Customer - [Not a customer?](#not-a-customer)
* Must have an account on the ServiceHub Web Portal - [Don't have an account?](#dont-have-an-account)
* Must have the 'Admin' level permissions in order to view the 'Company Settings' - [Not an Admin?](#not-an-admin)

## Getting Started

Here are a few steps to help you get started:

* [Getting an API Key](#getting-an-API-Key)
* [Creating an API Call](#creating-an-api-call)
    * [Authentication](#authentication)
    * [Example Call (Getting your Company)](#example-call-getting-your-company)
* [Understanding the Response](#understanding-the-response)
    * [Successful Response](#successful-response)
    * [Other Error Responses](#other-error-responses)
* [Additional Information](#additional-information)
* [Additional Endpoints](#additional-endpoints)

## Getting an API Key

Getting an API Key is done via the ServiceHub Web Portal, found at https://portal.digitalspace.co.uk/.

### Process

As long as all requirements have been met, you'll be able to generate your API Key.

 1. To generate an API Key you will need to login to the ServiceHub Web Portal at https://portal.digitalspace.co.uk/login.

 2. Navigate to the 'Credentials' page, under the 'Developer' Menu tab (as shown in the image below).

![](https://github.com/timicoltd/ServiceHub-Developer/blob/master/images/API%20Keys.png)
 
 3. Click the Generate API Key button.
 
 4. Provide the API Key name, this is for your reference only. It allows for you to refer to an API Key (as you may have many) without showing you the actual API Key.
 
 5. Once submitted, you will be shown your API Key for you to store securely and use whilst calling ServiceHub REST API.
 
_**Please note that you will only be able to see this key once and would need to regenerate the key if lost, so make a note of your API Key at this stage (and store it somewhere secure).**_

## Creating an API Call

Creating an API call is as simple as sending a https request.

### Authentication

All API calls need to be authenticated by your API Key as a Bearer Token.

To do so, you need to add the Authorization header to your request, with the value as **'Bearer {APIKEY}'** - Replacing {APIKEY} with your API Key from earlier.

```sh
$ curl -H "Authorization: Bearer {API KEY}" https://servicehub-api.digitalspace.co.uk/
```

### Example Call (Getting your Company)

We've made a simple testing endpoint that returns back the company tied to your API Key. 

The test endpoint would be a GET request to https://api.digitalspace.co.uk/company

```sh
$ curl -H "Authorization: Bearer {API KEY}" GET https://api.digitalspace.co.uk/company
```

The expected result would be a JSON Object, containing your Company's Name (as shown below)

```json
{
    "company": "Digital Space Group Ltd"
}
```

## Understanding the Response

Once you have made a call to the ServiceHub REST API, you will generally get a JSON Response however sometimes you will you just get a 200 Response (which is generally returned when you do a POST or PUT call and no data needs to be returned but confirmation that the call was successful.

### Successful Response

An example successful response (with a JSON object) would be:

```json
{
    "company": "Digital Space Group Ltd"
}
```

An example successful response (just the status code) would be:

```text
HTTP/1.1 200 OK
```

### Other Error Responses

From time to time, you may experience another response. These generally mean something went wrong but can be easily understood as to what happened.

#### HTTP/1.1 401 Unauthorized

You did not include a correct Authorization header or the bearer token is invalid.

```json
{
    "StatusCode": 401,
    "ExceptionMessage": "You must be authorized to view this resource."
}
```

#### HTTP/1.1 403 Forbidden

You included a correct Authorization header, but you don't have permission to perform the requested operation. (Whilst this error code shouldn't happen, since API Keys run at admin level and would have permission to all endpoints, there could be a time where a permission is missing and this would be returned

```json
{
    "StatusCode": 403,
    "ExceptionMessage": "You do not have permission to access this resource."
}
```

#### HTTP/1.1 404 Not Found

The request managed to reach the https://api.digitalspace.co.uk/ domain but the endpoint you specified was not found. This could be because of a spelling mistake, attempting to call an endpoint that doesn't exist or an incorrect request type.

```json
{
    "StatusCode": 404,
    "ExceptionMessage": "The resource you are looking for could have been removed, had its name changed, or is temporarily unavailable."
}
```

#### HTTP/1.1 500 Internal Server Error

An internal server error means that something went wrong on our end, though this is rare it could occasionally happen. We return the same JSON response format, a StatusCode and an ExceptionMessage like the other errors, though the message would be more specific (more for our usage).

```json
{
    "StatusCode": 500,
    "ExceptionMessage": "None Generic Error Message"
}
```

#### Other Error Responses

Other responses exist which indicate an error has occured, though generally rare and less generic than the ones above. They can include a none HTTP/1.1 standard error code, to indicate that this was expected due to a certain reason. These responses will follow the same response object from above, though could include a unique StatusCode and ExceptionMessage, to provide an overview of what has happened. 

An example would be from the Company endpoint

```json
{
    "StatusCode": 404,
    "ExceptionMessage": "No company can be found for this API Key."
}
```

Whilst an error has occured, it's known that it can, so we have caught it and provided a better understanding as to what has happened.


## Additional Information

### Not a Customer?

To use the ServiceHub REST API, you will need to be a customer of Digital Space. ServiceHub is a product which allows our customers to manage and view all aspects of a customers account. 

[ServiceHub Web Portal](https://portal.digitalspace.co.uk/) is our main product, which provides an online portal for you to view your account (or company if Admin level) as well as interact with us for support. 

[ServiceHub Developer](https://github.com/timicoltd/ServiceHub-Developer) is our extended version of the Web Portal, it allows for our customers to directly call our services for their own infrastructure and software, to benefit from the collaboration of services.

### Don't have an account?

So you're a customer of Digital Space but don't have a ServiceHub Account and wish to use our [ServiceHub Web Portal](https://portal.digitalspace.co.uk/) and our [ServiceHub Developer](https://github.com/timicoltd/ServiceHub-Developer).

If you head to the [ServiceHub Web Portal](https://portal.digitalspace.co.uk/login) and choose Register from the Login screen, you will be able to follow the process of registering for an account.

Once you have supplied your email address, and follow the link within your email, you'll be able to provide us with some information about who you are and set up your password for your account. If you are from a company which already has users with the ServiceHub Web Portal, and your company admin has setup approved domains, you will automatically be registered, otherwise you will be required to wait whilst a Digital Space memeber of staff can approve your request for an account and link you to tour company.

### Not an Admin?

So you have a Digital Space account but you're not an admin so cannot generate API Keys. This is easy enough to fix, if you're the developer for your company and cannot get Admin level access, then an Admin within the company can generate an API Key for you and provide it to you.

If you are allowed Admin level access to ServiceHub then you may raise a ticket to us, requesting for Admin level access for the purpose of generating API Keys. This should be granted within due time so long as you meet the requirements.

Once your ticket has been responded too and you are now an Admin, you should be able to generate API Keys, as outlined above.

## Additional Endpoints

Now that you have completed the ServiceHub REST API introduction, we have create other endpoints to get retrieve, create and manipulate other data:

* [Incidents](https://github.com/timicoltd/ServiceHub-Developer/blob/master/examples/curl/incident/README.md)
* [Requests](https://github.com/timicoltd/ServiceHub-Developer/blob/master/examples/curl/request/README.md)

These guides have detailed steps on how to call the specific endpoints and are the only guides Digital Space will provide on interacting with the ServiceHub REST API.
