# ServiceHub Web Hooks

Timico ServiceHub Web Hooks allows you to configure specific endpoints to which Timico send POST requests to based on event and trigger.

## Requirements

* Must be a Timico Customer - [Not a customer?](#not-a-customer)
* Must have an account on the ServiceHub Web Portal - [Don't have an account?](#dont-have-an-account)
* Must have the 'Admin' level permissions in order to view the 'Company Settings' - [Not an Admin?](#not-an-admin)


## Setting up a Web Hook

Configuring a Web Hook is done via the ServiceHub Web Portal, found at https://portal.timico.com.

### Process

As long as you meet all the requirements above you'll be able to configure your Web Hook.

 1. To configure a Web Hook you will need to login to the ServiceHub Web Portal at https://portal.timico.com/login.

 2. Navigate to the 'Web Hooks' page, under the 'Developer' Menu tab (as shown in the image below).

![](https://github.com/timicoltd/ServiceHub-Developer/blob/master/images/Web%20Hooks.png)
 
 3. Click the Configure Web Hooks button.
 
 4. Choose the source for your Web Hook (currently we only support Incidents and Requests) - The source would be upon what section of  ServiceHub would you like to be notified about.
 
 5. Choose the action for your Web Hook (currently we only support Create and Update) - The action would be the trigger for us to send a POST request to your web hook.
 
 6. Provide the url for your Web Hook, so we know where to send our POST request once your event has been triggered.
 
 _**Once all of the above steps have been completed, your Web Hook will be configured and ready for us to send POST requests to.**_
 
 
 ### An example Web Hook scenario would be:
 
 * Creating a Web Hook with the following:
    * Source = Incidents
    * Action = Create
    * URL = servicehub-api.timico.com/web-hooks/incident-created
    
When an **'Incident'** (Source) is **'Created'** (Action) with us at Timico, either via the [ServiceHub Web Portal](https://portal.timico.com/) or [ServiceHub REST API](https://github.com/timicoltd/ServiceHub-Developer/blob/master/examples/curl/incident/README.md#create-incident) then we would send a HTTP POST request to **'servicehub-api.timico.com/web-hooks/incident-created'** (URL), with a JSON object of the incident that has been created.
 

## Additional Information

### Not a Customer?

To use the ServiceHub Web Hooks, you will need to be a customer of Timico. ServiceHub is a product which allows our customers to manage and view all aspects of a customers account. 

[ServiceHub Web Portal](https://portal.timico.com) is our main product, which provides an online portal for you to view your account (or company if Admin level) as well as interact with us for support. 

[ServiceHub Developer](https://github.com/timicoltd/ServiceHub-Developer) is our extended version of the Web Portal, it allows for our customers to directly call our services for their own infrastructure and software, to benefit from the collaboration of services.

### Don't have an account?

So you're a customer of Timico but don't have a ServiceHub Account and wish to use our [ServiceHub Web Portal](https://portal.timico.com) and our [ServiceHub Developer](https://github.com/timicoltd/ServiceHub-Developer).

If you head to the [ServiceHub Web Portal](https://portal.timico.com/login) and choose Register from the Login screen, you will be able to follow the process of registering for an account.

Once you have supplied your email address, and follow the link within your email, you'll be able to provide us with some information about who you are and set up your password for your account. If you are from a company which already has users with the ServiceHub Web Portal, and your company admin has setup approved domains, you will automatically be registered, otherwise you will be required to wait whilst a Timico memeber of staff can approve your request for an account and link you to tour company.

### Not an Admin?

So you have a Timico account but you're not an admin so cannot configure Web Hooks. This is easy enough to fix, if you're the developer for your company and cannot get Admin level access, then an Admin within the company can set up your Web Hooks for you.

If you are allowed Admin level access to ServiceHub then you may raise a ticket to us, requesting for Admin level access for the purpose of configuring Web Hooks. This should be granted within due time so long as you meet the requirements.

Once your ticket has been responded too and you are now an Admin, you should be able to configure Web Hooks, as outlined above.
