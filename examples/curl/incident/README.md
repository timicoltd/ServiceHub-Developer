# ServiceHub-API (Incidents)

Timico ServiceHub-API allows you to call the Incident endpoint to get all incidents for your company, more information on a specific incident, create an incident, view comments for an incident and create new comments on an incident.

## Prerequisites

To be able to call the ServiceHub-API you will need to ensure that you can complete and call the example endpoint found in the [Getting Started](https://github.com/timicoltd/ServiceHub-API/) document. Calling this endpoint means that you have generated an API Key, made a basic call and understood the possible responses our API returns.

## Breakdown

Assuming you have passed the prerequisites, the follow are the possible endpoints you can call via the incident endpoint.

* [Get Incidents]()
* [Get Incident]()
* [Create Incident]()
* [Update Incident]()
* [Get Comments]()
* [Add Comment]()

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
