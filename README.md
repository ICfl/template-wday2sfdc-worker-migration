
<<<<<<< HEAD
# Anypoint Template: Workday Salesforce Worker Migration
=======
# Anypoint Template: Workday to Salesforce Worker Migration
>>>>>>> bf3bde4803f417ff7f9542604fd977fc0c331c89

+ [License Agreement](#licenseagreement)
+ [Use Case](#usecase)
+ [Considerations](#considerations)
	* [Salesforce Considerations](#salesforceconsiderations)
	* [Workday Considerations](#workdayconsiderations)
+ [Run it!](#runit)
	* [Running on premise](#runonopremise)
	* [Running on Studio](#runonstudio)
	* [Running on Mule ESB stand alone](#runonmuleesbstandalone)
	* [Running on CloudHub](#runoncloudhub)
	* [Deploying your Anypoint Template on CloudHub](#deployingyouranypointtemplateoncloudhub)
	* [Properties to be configured (With examples)](#propertiestobeconfigured)
+ [API Calls](#apicalls)
+ [Customize It!](#customizeit)
	* [config.xml](#configxml)
	* [businessLogic.xml](#businesslogicxml)
	* [endpoints.xml](#endpointsxml)
	* [errorHandling.xml](#errorhandlingxml)


# License Agreement <a name="licenseagreement"/>
Note that using this template is subject to the conditions of this [License Agreement](AnypointTemplateLicense.pdf).
Please review the terms of the license before downloading and using this template. In short, you are allowed to use the template for free with Mule ESB Enterprise Edition, CloudHub, or as a trial in Anypoint Studio.

# Use Case <a name="usecase"/>
As a Workday admin I want to migrate workers to Salesfoce.

<<<<<<< HEAD
This Anypoint Template should serve as a foundation for the process of migrating Worker from Workday instance to Salesforce, being able to specify filtering criteria and desired behaviour when a user already exists in the destination system. 
=======
This Anypoint Template should serve as a foundation for the process of migrating Worker from a Workday instance to Salesforce, being able to specify filtering criterias and desired behaviour when a user already exists in the destination system. 
>>>>>>> bf3bde4803f417ff7f9542604fd977fc0c331c89

As implemented, this Anypoint Template leverages the [Batch Module](http://www.mulesoft.org/documentation/display/current/Batch+Processing).
The batch job is divided in Input, Process and On Complete stages.
During the Input stage the Anypoint Template will go to the Workday and query all the existing active workers that match the filter criteria. The criteria is based on manipulations starting from the given date.
The last step of the Process stage will group the workers and create them in Salesforce.
Finally during the On Complete stage the Anypoint Template will both output statistics data into the console and send a notification email with the results of the batch excecution.

# Considerations <a name="considerations"/>

There are a couple of things you should take into account before running this Anypoint Template:
1. **Users cannot be deleted in SalesForce:** For now, the only thing to do regarding users removal is disabling/deactivating them, but this won't make the username available for a new user.
2. **Each user needs to be associated to a Profile:** SalesForce's profiles are what define the permissions the user will have for manipulating data and other users. Each SalesForce account has its own profiles. In this Anypoint Template you will find a processor labeled *setup Worker for upsert* where to set your Profile Ids from the source account. Note that for the integration test to run properly, you should change the constant *sfdc.profileId* in *mule.test.properties* to one that's valid in your source organization.
3. **Working with sandboxes for the same account**: Although each sandbox should be a completely different environment, Usernames cannot be repeated in different sandboxes, i.e. if you have a user with username *bob.dylan* in *sandbox A*, you will not be able to create another user with username *bob.dylan* in *sandbox B*. If you are indeed working with Sandboxes for the same SalesForce account you will need to map the source username to a different one in the target sandbox, for this purpose, please refer to the processor labeled *setup Worker for upsert*.
4. **Workday email uniqueness**: The email can be repeated for two or more accounts (or missing). Therefore Workday accounts with duplicate emails will be removed from processing in the Input stage.

<<<<<<< HEAD
**IMPORTANT**: Cloudhub currently supports JRE version 1.6_x. Please make sure that your application is not built with newer JRE version.
=======

>>>>>>> bf3bde4803f417ff7f9542604fd977fc0c331c89

## Salesforce Considerations <a name="salesforceconsiderations"/>

There may be a few things that you need to know regarding Salesforce, in order for this template to work.

In order to have this template working as expected, you should be aware of your own Salesforce field configuration.

###FAQ

 - Where can I check that the field configuration for my Salesforce instance is the right one?

    [Salesforce: Checking Field Accessibility for a Particular Field][1]

- Can I modify the Field Access Settings? How?

    [Salesforce: Modifying Field Access Settings][2]


[1]: https://help.salesforce.com/HTViewHelpDoc?id=checking_field_accessibility_for_a_particular_field.htm&language=en_US
[2]: https://help.salesforce.com/HTViewHelpDoc?id=modifying_field_access_settings.htm&language=en_US


### As destination of data

<<<<<<< HEAD
There are no particular considerations for this Anypoint Template regarding Siebel as data destination.
=======
There are no particular considerations for this Anypoint Template regarding Salesforce as data destination.
>>>>>>> bf3bde4803f417ff7f9542604fd977fc0c331c89


## Workday Considerations <a name="workdayconsiderations"/>

### As source of data

There are no particular considerations for this Anypoint Template regarding Workday as data origin.

<<<<<<< HEAD
# Run it! <a name="runit"/>
Simple steps to get Workday Salesforce Worker Migration running.
=======

# Run it! <a name="runit"/>
Simple steps to get Workday to Salesforce Worker Migration running.
>>>>>>> bf3bde4803f417ff7f9542604fd977fc0c331c89
In any of the ways you would like to run this Anypoint Template this is an example of the output you'll see after hitting the HTTP endpoint:

<pre>
<h1>Batch Process initiated</h1>
<b>ID:</b>6eea3cc6-7c96-11e3-9a65-55f9f3ae584e<br/>
<b>Records to Be Processed: </b>9<br/>
<b>Start execution on: </b>Mon Jan 13 18:05:33 GMT-03:00 2014
</pre>

## Running on premise <a name="runonopremise"/>
In this section we detail the way you have to run you Anypoint Temple on you computer.


### Where to Download Mule Studio and Mule ESB
First thing to know if you are a newcomer to Mule is where to get the tools.

+ You can download Mule Studio from this [Location](http://www.mulesoft.com/platform/mule-studio)
+ You can download Mule ESB from this [Location](http://www.mulesoft.com/platform/soa/mule-esb-open-source-esb)


### Importing an Anypoint Template into Studio
Mule Studio offers several ways to import a project into the workspace, for instance: 

+ Anypoint Studio generated Deployable Archive (.zip)
+ Anypoint Studio Project from External Location
+ Maven-based Mule Project from pom.xml
+ Mule ESB Configuration XML from External Location

You can find a detailed description on how to do so in this [Documentation Page](http://www.mulesoft.org/documentation/display/current/Importing+and+Exporting+in+Studio).


### Running on Studio <a name="runonstudio"/>
Once you have imported you Anypoint Template into Anypoint Studio you need to follow these steps to run it:

+ Locate the properties file `mule.dev.properties`, in src/main/resources
+ Complete all the properties required as per the examples in the section [Properties to be configured](#propertiestobeconfigured)
+ Once that is done, right click on you Anypoint Template project folder 
+ Hover you mouse over `"Run as"`
+ Click on  `"Mule Application"`


### Running on Mule ESB stand alone <a name="runonmuleesbstandalone"/>
Complete all properties in one of the property files, for example in [mule.prod.properties] (../blob/master/src/main/resources/mule.prod.properties) and run your app with the corresponding environment variable to use it. To follow the example, this will be `mule.env=prod`. 
After this, to trigger the use case you just need to hit the local http endpoint with the port you configured in your file. If this is, for instance, `9090` then you should hit: `http://localhost:9090/migrateworkers` and this will output a summary report and send it in the mail.

## Running on CloudHub <a name="runoncloudhub"/>
While [creating your application on CloudHub](http://www.mulesoft.org/documentation/display/current/Hello+World+on+CloudHub) (Or you can do it later as a next step), you need to go to Deployment > Advanced to set all environment variables detailed in **Properties to be configured** as well as the **mule.env**.
<<<<<<< HEAD
Once your app is all set and started, supposing you choose as domain name `sfdcusermigration` to trigger the use case you just need to hit `http://sfdcusermigration.cloudhub.io/migrateworkers` and report will be sent to the email configured.
=======
Once your app is all set and started, supposing you choose as domain name `wdayworkermigration` to trigger the use case you just need to hit `http://wdayworkermigration.cloudhub.io/migrateworkers` and report will be sent to the email configured.
>>>>>>> bf3bde4803f417ff7f9542604fd977fc0c331c89

### Deploying your Anypoint Template on CloudHub <a name="deployingyouranypointtemplateoncloudhub"/>
Mule Studio provides you with really easy way to deploy your Template directly to CloudHub, for the specific steps to do so please check this [link](http://www.mulesoft.org/documentation/display/current/Deploying+Mule+Applications#DeployingMuleApplications-DeploytoCloudHub)


## Properties to be configured (With examples) <a name="propertiestobeconfigured"/>
In order to use this Mule Anypoint Template you need to configure properties (Credentials, configurations, etc.) either in properties file or in CloudHub as Environment Variables. Detail list with examples:
### Application configuration
+ http.port `9090`
+ migration.startDate `"2014-09-12T00:00:00.000+0200"`

#### Workday Connector configuration
+ wday.user `admin@workday`
+ wday.password `secret`
+ wday.endpoint `https://impl-cc.workday.com/ccx/service/workday/Human_Resources/v21.1`

#### Salesforce Connector
+ sfdc.username `user@company.com`
+ sfdc.password `secret`
+ sfdc.securityToken `1234fdkfdkso20kw2sd`
+ sfdc.url `https://login.salesforce.com/services/Soap/u/28.0`
+ sfdc.profileId `00e200000015oKFAAY`

+ sfdc.localeSidKey `en_US`
+ sfdc.languageLocaleKey `en_US`
+ sfdc.timeZoneSidKey `America/New_York`
+ sfdc.emailEncodingKey `ISO-8859-1`

#### SMPT Services configuration
+ smtp.host `smtp.gmail.com`
+ smtp.port `587`
+ smtp.user `sender%40gmail.com`
+ smtp.password `secret`

# API Calls <a name="apicalls"/>
Salesforce imposes limits on the number of API Calls that can be made. Therefore calculating this amount may be an important factor to consider. The Anypoint Template calls to the API can be calculated using the formula:

***1 + X + X / 200***

Being ***X*** the number of Users to be synchronized on each run. 

The division by ***200*** is because, by default, Users are gathered in groups of 200 for each Upsert API Call in the commit step. Also consider that this calls are executed repeatedly every polling cycle.	

For instance if 10 records are fetched from origin instance, then 12 api calls will be made (1 + 10 + 1).


# Customize It!<a name="customizeit"/>
This brief guide intends to give a high level idea of how this Anypoint Template is built and how you can change it according to your needs.
As mule applications are based on XML files, this page will be organized by describing all the XML that conform the Anypoint Template.
Of course more files will be found such as Test Classes and [Mule Application Files](http://www.mulesoft.org/documentation/display/current/Application+Format), but to keep it simple we will focus on the XMLs.

Here is a list of the main XML files you'll find in this application:

* [config.xml](#configxml)
* [endpoints.xml](#endpointsxml)
* [businessLogic.xml](#businesslogicxml)
* [errorHandling.xml](#errorhandlingxml)


## config.xml<a name="configxml"/>
Configuration for Connectors and [Properties Place Holders](http://www.mulesoft.org/documentation/display/current/Configuring+Properties) are set in this file. **Even you can change the configuration here, all parameters that can be modified here are in properties file, and this is the recommended place to do it so.** Of course if you want to do core changes to the logic you will probably need to modify this file.

In the visual editor they can be found on the *Global Element* tab.


## businessLogic.xml<a name="businesslogicxml"/>
Functional aspect of the Anypoint Template is implemented on this XML, directed by one flow responsible of excecuting the logic.
For the pourpose of this particular Anypoint Template the *mainFlow* just executes the Batch Job which handles all the logic of it.
This flow has Exception Strategy that basically consists on invoking the *defaultChoiseExceptionStrategy* defined in *errorHandling.xml* file.



## endpoints.xml<a name="endpointsxml"/>
This is the file where you will found the inbound and outbound sides of your integration app.
This Anypoint Template has only an [HTTP Inbound Endpoint](http://www.mulesoft.org/documentation/display/current/HTTP+Endpoint+Reference) as the way to trigger the use case.

###  Inbound Flow
**HTTP Inbound Endpoint** - Start Report Generation
+ `${http.port}` is set as a property to be defined either on a property file or in CloudHub environment variables.
+ The path configured by default is `migrateworkers` and you are free to change for the one you prefer.
+ The host name for all endpoints in your CloudHub configuration should be defined as `localhost`. CloudHub will then route requests from your application domain URL to the endpoint.
<<<<<<< HEAD
+ The endpoint is configured as a *request-response* since as a result of calling it the response will be the total of Users migrated and filtered by the criteria specified.
=======
+ The endpoint is configured as a *request-response* since as a result of calling it the response will be the total of Workers migrated and filtered by the criteria specified.
>>>>>>> bf3bde4803f417ff7f9542604fd977fc0c331c89



## errorHandling.xml<a name="errorhandlingxml"/>
Contains a [Catch Exception Strategy](http://www.mulesoft.org/documentation/display/current/Catch+Exception+Strategy) that is only Logging the exception thrown (If so). As you imagine, this is the right place to handle how your integration will react depending on the different exceptions.



