# ServiceHub REST API (Configuration Items)

Timico ServiceHub REST API allows you to call the Configuration Items endpoint to get all the configuration items for your company.

**Please note that all API calls will be made as a 'super user' - which basically means an admin level user is created on behalf of your company and linked to your API Key(s). When any API call is made, fields such as 'Created By', 'Requested By' and 'Updated By' will be pre-populated with your API Key's user rather than a specific user from your company. A future update will bring functionality to allow these to be provided within a request object (so that specific user's within your company can be assigned to an Incident for example).**

## Prerequisites

To be able to call the ServiceHub REST API you will need to ensure that you can complete and call the example endpoint found in the [Getting Started](https://github.com/timicoltd/ServiceHub-Developer/blob/master/ServiceHub%20REST%20API%20-%20Introduction.md) document. Calling this endpoint means that you have generated an API Key, made a basic call and understood the possible responses our API returns.

## Breakdown

Assuming you have passed the prerequisites, the follow are the possible endpoints you can call via the configuration items endpoint.

* [Get Configuration Items](#get-configuration-items)

Retrieve all configuration items for your company by sending a POST Request to https://servicehub-api-2.timico.com/cmdb

```sh
$ curl -H "Authorization: Bearer {API KEY}" GET https://servicehub-api-2.timico.com/cmdb
```
The expected result would be a JSON Object containing an array , to which would contain a list of objects (configuration items). An example response would be:

```json
[
    {
        "sysId": "000056aa1b7c14106d10262c721bd4bcb05",
        "company": "Test Company",
        "name": "Test Item",
        "SysClassName": "Radius Account",
        "XScloScilogicId": "",
        "ipAddress": "71.73.17.93",
        "ModelId.displayName": "",
        "serialNumber": "",
        "uDeviceNetworkId": "",
        "uMake": "",
        "installStatus": "Installed",
        "macAddress": "",
        "manufacturer": "",
        "vendor": "",
        "location": ""
    }
]
```

A breakdown of this response is:

* **SysID** - The identification number for this Configuration Item.
* **Name** - This is the Assignment Group name.
* **SysClassName** - Configuration item type.
* **InstallStatus** - The status of the Configuration item.

All other fields are more self explanatory as to what they represent.

