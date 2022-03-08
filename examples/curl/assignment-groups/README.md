# ServiceHub REST API (Assignment Groups)

Digital Space ServiceHub REST API allows you to call the Assignment groups endpoint to get all assignment groups for your company.

**Please note that all API calls will be made as a 'super user' - which basically means an admin level user is created on behalf of your company and linked to your API Key(s). When any API call is made, fields such as 'Created By', 'Requested By' and 'Updated By' will be pre-populated with your API Key's user rather than a specific user from your company. A future update will bring functionality to allow these to be provided within a request object (so that specific user's within your company can be assigned to an Incident for example).**

## Prerequisites

To be able to call the ServiceHub REST API you will need to ensure that you can complete and call the example endpoint found in the [Getting Started](https://github.com/timicoltd/ServiceHub-Developer/blob/master/ServiceHub%20REST%20API%20-%20Introduction.md) document. Calling this endpoint means that you have generated an API Key, made a basic call and understood the possible responses our API returns.

## Breakdown

Assuming you have passed the prerequisites, the follow are the possible endpoints you can call via the assignment groups endpoint.

* [Get Assignment Groups](#get-assignment-groups)
* [Get Assignment Group](#get-assignment-group)

All of the calls above require an Authorization Bearer token (API Key).

## Get Assignment Groups

Retrieve all assignment groups for your company by sending a GET Request to https://servicehub-api-2.digitalspace.co.uk/assignment-groups

```sh
$ curl -H "Authorization: Bearer {API KEY}" GET https://servicehub-api-2.digitalspace.co.uk/assignment-groups
```

The expected result would be a JSON Object containing an array , to which would contain a list of objects (assignment groups). An example response would be:

```json
[
    {
        "sysId": "f1e8a7c11b65224d091bfdb5be254bc2b4e",
        "name": "AssignmentGroupTest",
        "description": "Test assignment group description"
    }
]
```
A breakdown of this response is:

* **SysID** - The identification number for this Assignment Group (this sysID would be used in future calls and is used to address a certain assignment group via the API).
* **Name** - This is the Assignment Group name.
* **Description** - A brief description of the Assignment Group.

## Get Assignment Group

Retrieve information for a single Assignment Group by sending a GET Request to https://servicehub-api-2.digitalspace.co.uk/assignment-groups/{id}

```sh
$ curl -H "Authorization: Bearer {API KEY}" GET https://servicehub-api-2.digitalspace.co.uk/assignment-groups/{id}
```

Where replacing the {id} for the Assignment Group identification number, retrieved in the [Get Assignment Groups](#get-assignment-groups) endpoint example.

Using the ID from above, the complete call would be:

```sh
$ curl -H "Authorization: Bearer {API KEY}" GET https://servicehub-api-2.digitalspace.co.uk/assignment-groups/f1e8a7c11b65224d091bfdb5be254bc2b4e
```

The expected response would be a JSON Object representing the Assignment Group you have called.

```json
[
    {
        "sysId": "f1e8a7c11b65224d091bfdb5be254bc2b4e",
        "name": "AssignmentGroupTest",
        "description": "Test assignment group description"
    }
]
```

## Response Errors

Sometimes you may not get the expected response outlined above, instead you may get an error!

Whilst this is not what we want to return to you, sometimes there is a valid reason as to why you would get one.

For more a detailed breakdown of the kind of errors we may return to you, take a look at our [Other Error Responses](https://github.com/timicoltd/ServiceHub-Developer/blob/master/ServiceHub%20REST%20API%20-%20Introduction.md#other-error-responses) section.
