# ServiceHub-API (Incidents)

Timico ServiceHub-API allows you to call the Incident endpoint to get all incidents for your company, more information on a specific incident, create an incident, view comments for an incident and create new comments on an incident.

## Prerequisites

To be able to call the ServiceHub-API you will need to ensure that you can complete and call the example endpoint found in the [Getting Started](https://github.com/timicoltd/ServiceHub-API/) document. Calling this endpoint means that you have generated an API Key, made a basic call and understood the possible responses our API returns.

## Breakdown

Assuming you have passed the prerequisites, the follow are the possible endpoints you can call via the incident endpoint.

* [Get Incidents](#get-incidents)
* [Get Incident](#get-incident)
* [Create Incident](#create-incident)
* [Update Incident](#update-incident)
* [Get Comments](#get-comments)
* [Add Comment](#add-comment)

All of the calls above require an Authorization Bearer token (API Key).

## Get Incidents

Retrieve all incidents for your company by sending a GET Request to https://servicehub-api.timico.com/incident

```sh
$ curl -H "Authorization: Bearer {API KEY}" GET https://servicehub-api.timico.com/incident
```

The expected result would be a JSON Object containing an array (called results), to which would contain a list of objects (Incidents). An example response would be:

```json
{
    "results": [
        {
            "id": "98s9df8b9d9fd98gs983jk209320kjhr32",
            "number": "INC0000000",
            "shortDescription": "Short Description",
            "description": "Incident Description",
            "priority": "3 - Moderate",
            "state": "New",
            "category": "Inquiry / Help",
            "lastUpdated": null,
            "updatedBy": "company.api.key.name",
            "openedAt": "03/04/2019 11:21:37",
            "active": true,
            "createdBy": "company.api.key.name",
            "createdOn": "2019-04-03T11:21:37",
            "closureNotes": "",
            "resolvedBy": "",
            "resolvedAt": null
        }
    ]
}
```

A breakdown of this response is:

* **ID** - The identification number for this incident (this ID would be used in future calls and is used to address a certain Incident via the API).
* **Number** - This is the Incident reference number (this is used for referencing the Incident via the ServiceHub Web Portal and with Timico staff).
* **Short Description** - A brief description of the Incident that has been raised.
* **Description** - A full description of the Incident (to be aid the resolution of the Incident).
* **Priority** - Depending on the context, an Incident is given a priority number.
* **State** - What state is the Inciddent in, this could be 'New' or 'Closed' for example.
* **Category** - Which Category this Incident falls within.

All other fields are more self explanatory as to what they represent.

## Get Incident

Retrieve information for a single Incident by sending a GET Request to https://servicehub-api.timico.com/incident/{id}

```sh
$ curl -H "Authorization: Bearer {API KEY}" GET https://servicehub-api.timico.com/incident/{id}
```

Where replacing the {id} for the Incident identification number, retrieved in the [Get Incidents](#get-incidents) endpoint example.

Using the ID from above, the complete call would be:

```sh
$ curl -H "Authorization: Bearer {API KEY}" GET https://servicehub-api.timico.com/incident/98s9df8b9d9fd98gs983jk209320kjhr32
```

The expected response would be a JSON Object representing the Incident you have called.

```json
{
    "id": "98s9df8b9d9fd98gs983jk209320kjhr32",
    "number": "INC0000000",
    "shortDescription": "Short Description",
    "description": "Incident Description",
    "priority": "3 - Moderate",
    "state": "New",
    "category": "Inquiry / Help",
    "lastUpdated": null,
    "updatedBy": "company.api.key.name",
    "openedAt": "03/04/2019 11:21:37",
    "active": true,
    "createdBy": "company.api.key.name",
    "createdOn": "2019-04-03T11:21:37",
    "closureNotes": "",
    "resolvedBy": "",
    "resolvedAt": null
}
```

A breakdown of this response is:

* **ID** - The identification number for this incident (this ID would be used in future calls and is used to address a certain Incident via the API).
* **Number** - This is the Incident reference number (this is used for referencing the Incident via the ServiceHub Web Portal and with Timico staff).
* **Short Description** - A brief description of the Incident that has been raised.
* **Description** - A full description of the Incident (to be aid the resolution of the Incident).
* **Priority** - Depending on the context, an Incident is given a priority number.
* **State** - What state is the Inciddent in, this could be 'New' or 'Closed' for example.
* **Category** - Which Category this Incident falls within.

All other fields are more self explanatory as to what they represent.

## Create Incident

Create an Incident for Timico staff to handle, this allows for you to complete the same process available on the ServiceHub Web Portal but via our API, so you can develop your own system to submit an Incident for you.

You can create an Incident by sending a POST request to https://servicehub-api.timico.com/incident with a JSON Body.

### Request Object

You will need to send a JSON Object with this request, containing the follow (to complete the incident)

```json
{
	"ShortDescription" : "Please Provide Short Description Here",
	"Description" : "Please Provide Description Here",
	"Impact" : "What impact is this happening?"
}
```

The JSON object will need to be sent via a POST request, as shown:

```sh
$ curl -H "Authorization: Bearer {API KEY}" POST -d '{
    "ShortDescription" : "Please Provide Short Description Here",
	"Description" : "Please Provide Description Here",
	"Impact" : "What impact is this happening?"
}' https://servicehub-api.timico.com/incident
```

### Response Object

The expected response would be a JSON Object containing the newly created Incident.

```json 
{
    "id": "878945hfwjf8suf8sj8js8fus8uf9s8jfs0",
    "number": "INC0000000",
    "shortDescription": "Please Provide Short Description Here"
}
```
* **ID** - The identification number for this incident (this ID would be used in future calls and is used to address a certain Incident via the API).
* **Number** - This is the Incident reference number (this is used for referencing the Incident via the ServiceHub Web Portal and with Timico staff).
* **Short Description** - The same as the one you sent in the POST Request

## Update Incident

Whilst you cannot update information on an Incident, our view of updating an Incident is to Open/Close the Incident.

You can update an Incident by sending a PUT request to https://servicehub-api.timico.com/incident/{id} with a Update Incident JSON Object.

### Close an Incident

To close an Incident you need to send a PUT request to https://servicehub-api.timico.com/incident/{id} - with {id} being the identification number of the Incident.

You also need to provide a request object as follows:

```json
{
	"State" : "6",
	"CloseNotes" : "Why are you closing the Incident?"
}
```

* **State** - State should remain as '6' for closing a ticket.
* **CloseNotes** - Providing a description of why the Incident has been closed.

The JSON Object should be sent via a PUT request, as shown:

```sh
$ curl -H "Authorization: Bearer {API KEY}" PUT -d '{
	"State" : "6",
	"CloseNotes" : "Why are you closing the Incident?"
}' https://servicehub-api.timico.com/incident/98s9df8b9d9fd98gs983jk209320kjhr32
```

**You will not recieve a response object for this call, you will only get a HTTP/1.1 200 OK Response.**

### Reopen an Incident

Similar to Closing an Incident (since you make the exact same call), you just need to send a different state and no closure notes.

To reopen an Incident you need to send a PUT request to https://servicehub-api.timico.com/incident/{id} - with {id} being the identification number of the Incident.

You also need to provide a request object as follows:

```json
{
	"State" : "2"
}
```

* **State** - State should remain as '2' for reopening a ticket.

The JSON Object should be sent via a PUT request, as shown:

```sh
$ curl -H "Authorization: Bearer {API KEY}" PUT -d '{
	"State" : "2"
}' https://servicehub-api.timico.com/incident/98s9df8b9d9fd98gs983jk209320kjhr32
```

**You will not recieve a response object for this call, you will only get a HTTP/1.1 200 OK Response.**

## Get Comments

Knowing the Incident identification number, you can retrieve a list of all the comments.

To get comments for a specific incident you need to send a GET request to https://servicehub-api.timico.com/incident/{id}/comments - with {id} being the identification number of the Incident.

```sh
$ curl -H "Authorization: Bearer {API KEY}" GET https://servicehub-api.timico.com/incident/98s9df8b9d9fd98gs983jk209320kjhr32/comments
```

The expected response would be a JSON Object, containg an Array of a Comment Container, a comment container would contain the group name (representing the date of the comment, for when multiple comments are made on the same date) and another array of comments (Comment Object's).

```json
{
    "commentGroups": [
        {
            "groupName": "01/04/2019",
            "comments": [
                {
                    "id": "83bd55a1dbecf78000a3f9971d96190b",
                    "value": "Testing Comments from ServiceHub Customer API",
                    "ticketId": "98s9df8b9d9fd98gs983jk209320kjhr32",
                    "createdBy": "company.api.key.name",
                    "name": "incident",
                    "createdOn": "2019-04-01T10:59:07",
                    "userClassification": "User",
                    "type": null,
                    "body": null
                }
	     ]
	}
    ]
}
```
A breakdown of this response is:

* **Comment Groups** - Is an array of objects, grouped by the date of the comments.
	* **Group Name** - Is a String reference of the date of the comments.
	* **Comments** - Is an array of comment objects
		* **ID** - The identification number of the comment, used to reference a certain comment via the API.
		* **Value** - The value of the comment (what has been written)
		* **Ticket ID** - This is the identification number of the Incident, the same as in the request.

All other fields are more self explanatory as to what they represent, though Body and Type are normally null unless the comment was generated via an Email, in which case they will represent that and the comment value will be empty instead.

## Add Comment

Knowing the Incident identification number, you can add a comment to the incident.

To add a comment to a specific incident you need to send a POST request to https://servicehub-api.timico.com/incident/{id}/comment - with {id} being the identification number of the Incident.

You will need to send a JSON Object with this request, containing the following:

```json
{
	"Comments" : "Testing Comments from ServiceHub Customer API"
}
```

The JSON object will need to be sent via a POST request, as shown:

```sh
$ curl -H "Authorization: Bearer {API KEY}" POST -d '{
    "Comments" : "Testing Comments from ServiceHub Customer API"
}' https://servicehub-api.timico.com/incident/98s9df8b9d9fd98gs983jk209320kjhr32/comment
```

**You will not recieve a response object for this call, you will only get a HTTP/1.1 200 OK Response.**

## Response Errors

Sometimes you may not get the expected response outlined above, instead you may get an error!

Whilst this is not what we want to return to you, sometimes there is a valid reason as to why you would get one.

For more a detailed breakdown of the kind of errors we may return to you, take a look at our [Other Error Responses](https://github.com/timicoltd/ServiceHub-API#other-error-responses) section.
