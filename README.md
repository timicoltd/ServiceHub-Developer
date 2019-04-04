# ServiceHub-API

Timico ServiceHub-API requires a Timico customer account at https://portal.timico.com and a registered API Key via the ServiceHub Web Portal. Guidence for acquiring an API Key will be below.

## Getting Started

Here are a few steps to help you get started:

* [Getting an API Key]()
* [Creating an API Call]()
    * [Authentication]()
    * [Example Call (Getting your Company)]()
* [Understanding the Response]()
    * [Successful Response]()
    * [Other Error Responses]()

## Getting an API Key

Getting an API Key is done via the ServiceHub Web Portal, found at https://portal.timico.com.

### Requirements

* Must be a Timico Customer - [Are not a customer?]()
* Must have an account on the ServiceHub Web Portal - [Don't have an account?]()
* Must have the 'Admin' level permissions in order to view the 'Company Settings' - [Not an Admin?]()

### Process

As long as all requirements have been met, you'll be able to generate your API Key.

 1. To generate an API Key you will need to login to the ServiceHub Web Portal at https://portal.timico.com/login.

 2. Navigate to the 'Settings' page, under the 'Company' Menu tab (as shown in the image below).

![](https://github.com/timicoltd/ServiceHub-API/blob/master/GitHub/Company-Settings.png)

 3. Select the 'Developer' Heading.
 
 4. Click the Generate API Key button.
 
 5. Provide the API Key name, this is for your reference only. It allows for you to refer to an API Key (as you may have many) without showing you the actual API Key.
 
 6. Once submitted, you will be shown your API Key for you to store securely and use whilst calling ServiceHub API.
 
_**Please note that you will only be able to see this key once and would need to regenerate the key if lost, so make a note of your API Key at this stage (and store it somewhere secure).**_

## Creating an API Call

Creating an API call is as simple as sending a https request.

### Authentication

All API calls need to be authenticated by your API Key as a Bearer Token.

To do so, you need to add the Authorization header to your request, with the value as **'Bearer {APIKEY}'** - Replacing {APIKEY} with your API Key from earlier.

```sh
$ curl -H "Authorization: Bearer {API KEY}" https://servicehub-api.timico.com/
```

### Example Call (Getting your Company)

We've made a simple testing endpoint that returns back the company tied to your API Key. 

The test endpoint would be a GET request to https://servicehub-api.timico.com/company

```sh
$ curl -H "Authorization: Bearer {API KEY}" https://servicehub-api.timico.com/company
```

The expected result would be a JSON Object, containing your Company's Name (as shown below)

```json
{
    "company": "Timico Ltd"
}
```

## Understanding the Response

Once you have made a call to the ServiceHub API, you will generally get a JSON Response however sometimes you will you just get a 200 Response (which is generally returned when you do a POST or PUT call and no data needs to be returned but confirmation that the call was successful.

### Successful Response

An example successful response (with a JSON object) would be:

```json
{
    "company": "Timico Ltd"
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

The request managed to reach the https://servicehub-api.timico.com/ domain but the endpoint you specified was not found. This could be because of a spelling mistake, attempting to call an endpoint that doesn't exist or an incorrect request type.

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
