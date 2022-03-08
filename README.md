# ServiceHub Developer

Digital Space ServiceHub Developer allows for Digital Space customers to connect to and manage Digital Space data, specific to their company.

To use and benefit from the ServiceHub Developer product, we allow two methods of integration; ServiceHub REST API (where we have made specific restful endpoints for you to call) and ServiceHub Web Hooks (where you provide us the dedicated url and event you wish to be notified about).

_**Please note; Digital Space do not provide technical support other than the documentation on the [ServiceHub Developer GitHub](https://github.com/timicoltd/ServiceHub-Developer) of how to use and integrate the ServiceHub Developer product.**_

## Prerequisites / Requirements

There are a couple of prerequisites / requirements before being able to use the ServiceHub Developer product:

* Must be a Digital Space Customer - [Not a customer?](#not-a-customer)
* Must have an active and registered account on the ServiceHub Web Portal - [Don't have an account?](#dont-have-an-account)
* Must have the 'Admin' level permissions in order to view the 'Developer' section on the ServiceHub Web Portal - [Not an Admin?](#not-an-admin)

## ServiceHub REST API

The ServiceHub REST API allows for developers to make POST, GET, PUT, DELETE requests to specifically designed endpoints, these calls will allow for the developer to retrieve, manipulate or create data for their company (based on the endpoint specified as to what data is affected).

For an introduction to the ServiceHub REST API and to get started with creating your API Key, creating a mock call and understanding the responses you may get, follow the [ServiceHub REST API - Introduction](https://github.com/timicoltd/ServiceHub-Developer/blob/master/ServiceHub%20REST%20API%20-%20Introduction.md)

Currently documented and publicly accessible endpoints are:

* [Getting your Company](https://github.com/timicoltd/ServiceHub-Developer/blob/master/ServiceHub%20REST%20API%20-%20Introduction.md#example-call-getting-your-company)
* [Incident](https://github.com/timicoltd/ServiceHub-Developer/blob/master/examples/curl/incident/README.md)
* [Request](https://github.com/timicoltd/ServiceHub-Developer/blob/master/examples/curl/request/README.md)

These have breakdowns of how to make all possible calls within that specified endpoint, follow the linked 'read me' documentation above to learn more about making calls to those endpoints.

## ServiceHub Web Hooks

The ServiceHub Web Hooks allows for developers to be notified upon certain events that happen with Digital Space. Rather than creating a polling system with our ServiceHub REST API, you will be able to retrieve a POST request on a dedicated endpoint (hosted and created by yourself) with the related data based on the event and trigger you specified.

For an introduction to the ServiceHub Web Hooks and to get started with setting up your Web Hooks, follow the [ServiceHub Web Hooks - Introduction](https://github.com/timicoltd/ServiceHub-Developer/blob/master/ServiceHub%20Web%20Hooks%20-%20Introduction.md)

## Additional Information

### Not a Customer?

To use ServiceHub Developer, you will need to be a customer of Digital Space. ServiceHub is a product which allows our customers to manage and view all aspects of a customers account. 

[ServiceHub Web Portal](https://portal.timico.com) is our main product, which provides an online portal for you to view your account (or company if Admin level) as well as interact with us for support. 

[ServiceHub Developer](https://github.com/timicoltd/ServiceHub-Developer) is our extended version of the Web Portal, it allows for our customers to directly call our services for their own infrastructure and software, to benefit from the collaboration of services.

### Don't have an account?

So you're a customer of Digital Space but don't have a ServiceHub Account and wish to use our [ServiceHub Web Portal](https://portal.digitalspace.co.uk/) and our [ServiceHub Developer](https://github.com/timicoltd/ServiceHub-Developer).

If you head to the [ServiceHub Web Portal](https://portal.digitalspace.co.uk/login) and choose Register from the Login screen, you will be able to follow the process of registering for an account.

Once you have supplied your email address, and follow the link within your email, you'll be able to provide us with some information about who you are and set up your password for your account. If you are from a company which already has users with the ServiceHub Web Portal, and your company admin has setup approved domains, you will automatically be registered, otherwise you will be required to wait whilst a Digital Space memeber of staff can approve your request for an account and link you to tour company.

### Not an Admin?

So you have a Digital Space account but you're not an admin so cannot make use of the ServiceHub Developer functionality. This is easy enough to fix, if you're the developer for your company and cannot get Admin level access, then an Admin within the company can do those steps on your behalf.

If you are allowed Admin level access to ServiceHub then you may raise a ticket to us, requesting for Admin level access for the purpose of using the ServiceHub Developer functionality. This should be granted within due time so long as you meet the requirements.

Once your ticket has been responded too and you are now an Admin, you will be able to configure everything needed for ServiceHub Developer products.
