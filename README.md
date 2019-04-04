# ServiceHub-API

Timico ServiceHub-API requires a Timico customer account at https://portal.timico.com and a registered API Key via the ServiceHub Web Portal. Guidence for acquiring an API Key will be below.

## Getting Started

Here are a few steps to help you get started:

* [Getting an API Key]()
* [Creating an API Call]()
    * [Authentication]()
    * [Example Call (Getting your Company)]()
* [Understanding the Response]()

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

We've made a simple testing endpoint that returns back the company you are requesting for. 

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
