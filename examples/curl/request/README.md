# ServiceHub REST API (Requests)

Timico ServiceHub REST API allows you to call the Request endpoint to get all requests for your company, more information on a specific request, create a request, view comments for a request and create new comments on a request.

**Please note that all API calls will be made as a 'super user' - which basically means an admin level user is created on behalf of your company and linked to your API Key(s). When any API call is made, fields such as 'Created By', 'Requested By' and 'Updated By' will be pre-populated with your API Key's user rather than a specific user from your company. A future update will bring functionality to allow these to be provided within a request object (so that specific user's within your company can be assigned to an Incident for example).**

## Prerequisites

To be able to call the ServiceHub REST API you will need to ensure that you can complete and call the example endpoint found in the [Getting Started](https://github.com/timicoltd/ServiceHub-Developer/blob/master/ServiceHub%20REST%20API%20-%20Introduction.md) document. Calling this endpoint means that you have generated an API Key, made a basic call and understood the possible responses our API returns.

## Breakdown

Assuming you have passed the prerequisites, the follow are the possible endpoints you can call via the request endpoint.

* [Get Requests](#get-requests)
* [Get Request](#get-request)
* [Get Catalog Items](#get-catalog-items)
* [Get Catalog Item Variables](#get-catalog-item-variables)
* [Create Request](#create-request)
* [Create Call](#create-call)
* [Update Request Item](#update-request-item)
* [Get Comments](#get-comments)
* [Add Comment](#add-comment)
* [Add Attachment](#add-attachment)

All of the calls above require an Authorization Bearer token (API Key).

## Get Requests

Retrieve all requests for your company by sending a GET Request to https://servicehub-api-2.timico.com/request

```sh
$ curl -H "Authorization: Bearer {API KEY}" GET https://servicehub-api-2.timico.com/request
```

The expected result would be a JSON Object containing an array (called results), to which would contain a list of objects (Requests). An example response would be:

```json
{
    "results": [
        {
            "id": "93984njfidjifdigna989fj9jfuua9h8",
            "description": "Request Description",
            "shortDescription": "Short Description",
            "state": "Open",
            "openedAt": "2019-04-01T11:37:07",
            "requestItemNumber": "RITM0000000",
            "requestNumber": "REQ0000000",
            "requestedFor": "company.api.key.name",
            "active": true
        }
    ]
}
```

A breakdown of this response is:

* **ID** - The identification number for this request (this ID would be used in future calls and is used to address a certain Request via the API).
* **Request Item Number** - This is the Request Item reference number (this is used for referencing the Request Item's of a Request via the ServiceHub Web Portal and with Timico staff).
* **Request Number** - This is the Request reference number (this is used for referencing the Request via the ServiceHub Web Portal and with Timico staff).
* **Short Description** - A brief description of the Request that has been raised.
* **Description** - A full description of the Request.
* **State** - What state is the Request in, this could be 'New' or 'Closed' for example.

All other fields are more self explanatory as to what they represent.

## Get Request

Retrieve information for a single Request by sending a GET Request to https://servicehub-api-2.timico.com/request/{id}

```sh
$ curl -H "Authorization: Bearer {API KEY}" GET https://servicehub-api-2.timico.com/request/{id}
```

Where replacing the {id} for the Request identification number, retrieved in the [Get Requests](#get-requests) endpoint example.

Using the ID from above, the complete call would be:

```sh
$ curl -H "Authorization: Bearer {API KEY}" GET https://servicehub-api-2.timico.com/request/93984njfidjifdigna989fj9jfuua9h8
```

The expected response would be a JSON Object representing the Request you have called.

```json
{
    "id": "93984njfidjifdigna989fj9jfuua9h8",
    "description": "Request Description",
    "shortDescription": "Short Description",
    "state": "Open",
    "openedAt": "2019-04-01T11:37:07",
    "requestItemNumber": "RITM0000000",
    "requestNumber": "REQ0000000",
    "requestedFor": "company.api.key.name",
    "active": true
}
```
* **ID** - The identification number for this request (this ID would be used in future calls and is used to address a certain Request via the API).
* **Request Item Number** - This is the Request Item reference number (this is used for referencing the Request Item's of a Request via the ServiceHub Web Portal and with Timico staff).
* **Request Number** - This is the Request reference number (this is used for referencing the Request via the ServiceHub Web Portal and with Timico staff).
* **Short Description** - A brief description of the Request that has been raised.
* **Description** - A full description of the Request.
* **State** - What state is the Request in, this could be 'New' or 'Closed' for example.

All other fields are more self explanatory as to what they represent.

## Get Catalog Items

Retrieve all catalog items for your company by sending a GET Request to https://servicehub-api-2.timico.com/request/catalog-item

```sh
$ curl -H "Authorization: Bearer {API KEY}" GET https://servicehub-api-2.timico.com/request/catalog-item
```

The expected result would be a JSON Object containing an array, to which would contain a list of objects (catalog items). An example response would be:

```json
[
	{
		"SysId" : "83bd55a1dbecf78000a3f9971d96190b",
		"Name" : "Test Catalog item",
		"Description" : "Test Description"
	}
]
```

A breakdown of this response is:

* **SysId** - The identification number for this catalog item (this ID would be used in future calls and is used to address a certain catalog item via the API).
* **Name** - The name of this catalog item.
* **Description** - A full description of the catalog item.

## Get Catalog Item Variables

Retrieve all catalog item variables for a single catalog item by sending a POST Request to https://servicehub-api-2.timico.com/request/catalog-item-variables/{id}

```sh
$ curl -H "Authorization: Bearer {API KEY}" POST https://servicehub-api-2.timico.com/request/catalog-item-variables/{id}
```

Where replacing the {id} for the Catalog item identification number, retrieved in the [Get Catalog Items](#get-catalog-items) endpoint example.

Using the ID from above, the complete call would be:

```sh
$ curl -H "Authorization: Bearer {API KEY}" POST https://servicehub-api-2.timico.com/catalog-item-variables/98s9df8b9d9fd98gs983jk209320kjhr32
```

The expected result would be a JSON Object containing an array, to which would contain a list of objects (variables). An example response would be:
```json
[
	{
		"Name" : "u_test",
		"Type" : "dropdown",
		"QuestionText" : "This is a test variable",
		"Mandatory" : "true"
	}
]
```

A breakdown of this response is:

* **Name** - The internal name of the variable. (to be used as reference when creating a request).
* **Type** - Variable type. 
* **QuestionText** - The display name of the variable. 
* **Mandatory** - Variable is mandatory when creating the request.


## Create Request

Create a Request for Timico staff to handle, this allows for you to complete the same process available on the ServiceHub Web Portal but via our API, so you can develop your own system to submit a Request for you.

You can create a Request by sending a POST request to https://servicehub-api-2.timico.com/request/{id} with a JSON Body.

Where replacing the {id} for the Catalog item identification number, retrieved in the [Get Catalog Items](#get-catalog-items) endpoint example.

You will need to send a JSON Object with this request, containing the following:

```json
{
	"Variables" : 
	[
		{
			"Name" : "Variable name",
			"Value" : "Variable value",
		}
	]
}
```

The JSON object will need to be sent via a POST request, as shown:

```sh
$ curl -H "Authorization: Bearer {API KEY}" POST -d '{
    "Variables" : 
	[
		{
			"Name" : "Variable name",
			"Value" : "Variable value",
		}
	]
}' https://servicehub-api-2.timico.com/request/98s9df8b9d9fd98gs983jk209320kjhr32
```
### Response Object

The expected response would be a JSON Object containing the newly created Request.

```json 
{
    "RequestId": "878945hfwjf8suf8sj8js8fus8uf9s8jfs0",
    "RequestNumber" : "REQ0000000",
    "RequestItemId" : "12331224asjgdss8js8fus8uf9s833fgsd"
    "RequestItemNumber : "RITM0300002"
}
```

* **RequestId** - The identification number for this Request.
* **RequestNumber** - This is the Request reference number.
* **RequestItemId** - The identification number for the Request Item.
* **RequestItemNumber** - The Request Item reference number.


## Create Call

Create a Call request for Timico staff to handle, this allows for you to complete the same process available on the ServiceHub Web Portal but via our API, so you can develop your own system to submit a Call request for you.

You can create a Request by sending a POST request to https://servicehub-api-2.timico.com/request with a JSON Body.

### Call Object

You will need to send a JSON Object with this request, containing the follow:

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
}' https://servicehub-api-2.timico.com/request
```

### Response Object

The expected response would be a JSON Object containing the newly created Call (to be triaged into a Request by Timico Staff).

```json 
{
    "id": "984hfdu9fjd98fks938knca99893mj9uy741n",
    "number": "CALL0000000",
    "createdOn": "2019-04-04T15:19:26",
    "shortDescription": "Please Provide Short Description Here"
}
```
* **ID** - The identification number for this call (this ID would be used in future calls and is used to address a certain calls via the API).
* **Number** - This is the Call's reference number (this is used for referencing the call via the ServiceHub Web Portal and with Timico staff).
* **Short Description** - The same as the one you sent in the POST Request

## Update Request Item

You can update a Request item by sending a PUT request to https://servicehub-api-2.timico.com/request/{id} with a Update Request Item JSON Object.

### Close a Request Item

To close a Request Item you need to send a PUT request to https://servicehub-api-2.timico.com/request/{id} - with {id} being the identification number of the Request Item.

You also need to provide a request object as follows:

```json
{
	"State" : "3",
	"CloseNotes" : "Why are you closing the Request Item?"
}
```

* **State** - State should remain as '3' for closing a request item.
* **CloseNotes** - Providing a description of why the Request Item has been closed.

The JSON Object should be sent via a PUT request, as shown:

```sh
$ curl -H "Authorization: Bearer {API KEY}" PUT -d '{
	"State" : "3",
	"CloseNotes" : "Why are you closing the Request Item?"
}' https://servicehub-api-2.timico.com/request/98s9df8b9d9fd98gs983jk209320kjhr32
```
**You will not recieve a response object for this call, you will only get a HTTP/1.1 200 OK Response.**

### Reopen a Request Item

Similar to Closing a Request Item (since you make the exact same call), you just need to send a different state and no closure notes.

To reopen a Request Item you need to send a PUT request to https://servicehub-api-2.timico.com/request/{id} - with {id} being the identification number of the Request Item.

You also need to provide a request object as follows:

```json
{
	"State" : "2"
}
```

* **State** - State should remain as '2' for reopening a request item.

The JSON Object should be sent via a PUT request, as shown:

```sh
$ curl -H "Authorization: Bearer {API KEY}" PUT -d '{
	"State" : "2"
}' https://servicehub-api-2.timico.com/request/98s9df8b9d9fd98gs983jk209320kjhr32
```

**You will not recieve a response object for this call, you will only get a HTTP/1.1 200 OK Response.**

### Update Assignment Group 

To update the assignment group on a request item you need to send a PUT request to https://servicehub-api-2.timico.com/request/{id} - with {id} being the identification number of the Request Item.

You also need to provide a request object as follows:

```json
{
	"AsignmentGroup" : "Assignment Group Identification number",
}
```
The JSON Object should be sent via a PUT request, as shown:

```sh
$ curl -H "Authorization: Bearer {API KEY}" PUT -d '{
	"AsignmentGroup" : "Assignment Group Identification number",
}' https://servicehub-api-2.timico.com/request/98s9df8b9d9fd98gs983jk209320kjhr32
```

**You will not recieve a response object for this call, you will only get a HTTP/1.1 200 OK Response.**

## Get Comments

Knowing the Request identification number, you can retrieve a list of all the comments.

To get comments for a specific request you need to send a GET request to https://servicehub-api-2.timico.com/request/{id}/comments - with {id} being the identification number of the Request.

```sh
$ curl -H "Authorization: Bearer {API KEY}" GET https://servicehub-api-2.timico.com/request/93984njfidjifdigna989fj9jfuua9h8/comments
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
                    "ticketId": "93984njfidjifdigna989fj9jfuua9h8",
                    "createdBy": "company.api.key.name",
                    "name": "sc_req_item",
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
		* **Ticket ID** - This is the identification number of the Request, the same as in the request.

All other fields are more self explanatory as to what they represent, though Body and Type are normally null unless the comment was generated via an Email, in which case they will represent that and the comment value will be empty instead.

## Add Comment

Knowing the Request identification number, you can add a comment to the request.

To add a comment to a specific request you need to send a POST request to https://servicehub-api-2.timico.com/request/{id}/comment - with {id} being the identification number of the Request.

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
}' https://servicehub-api-2.timico.com/request/98s9df8b9d9fd98gs983jk209320kjhr32/comment
```

## Add Attachment

Knowing the Request item identification number, you can attach files to the request item.

To attach files to a specific request item you need to send a POST request to https://servicehub-api-2.timico.com/request/{id}/attachment - with {id} being the identification number of the request item.

You will need to send a JSON Object with this request, containing the following:

```json
{
	"Files" : 
	[
		{
			"Base64Encoding" : "The file encoded in a base64 string",
			"Name" : "Name of the file",
			"ContentType" : "Content type"
		}
	]
}
```

The JSON object will need to be sent via a POST request, as shown:

```sh
$ curl -H "Authorization: Bearer {API KEY}" POST -d '{
    "Files" : 
	[
		{
			"Base64Encoding" : "The file encoded in a base64 string",
			"Name" : "Name of the file",
			"ContentType" : "Content type"
		}
	]
}' https://servicehub-api-2.timico.com/request/98s9df8b9d9fd98gs983jk209320kjhr32/attachment
```
**The maximum size limit for a file is 2MB.** 

**You will not recieve a response object for this call, you will only get a HTTP/1.1 200 OK Response.**

## Response Errors

Sometimes you may not get the expected response outlined above, instead you may get an error!

Whilst this is not what we want to return to you, sometimes there is a valid reason as to why you would get one.

For more a detailed breakdown of the kind of errors we may return to you, take a look at our [Other Error Responses](https://github.com/timicoltd/ServiceHub-Developer/blob/master/ServiceHub%20REST%20API%20-%20Introduction.md#other-error-responses) section.
