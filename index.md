index page

Testing ...

![Image of LeanSwift](images/LeanSwift-Logo-HQ.png)<!-- .element height="50%" width="50%" -->


## LeanSwift HubSpot M3 Connector: User Guide

## Overview

This is a web application that enables customer creation synchronization from HubSpot to Infor M3. Whenever a new company is created in HubSpot, respective customer record gets created in Infor M3 via ION APIs.

**Test Link** : [https://hubspotm3connectordev.leanswift.com/](https://hubspotm3connectordev.leanswift.com/)

**Production Link** : <span style="color: red;">TBD</span>

Steps involved in enabling this integration are explained in this document.

## Step 1:

Install HubSpot client for HubSpotM3Connector by clicking on the following link.

**Test Link** : [https://app.hubspot.com/oauth/authorize?client\_id=9baffc4b-c9ad-4904-be3c-ea6bc0edc439&amp;redirect\_uri=http://localhost&amp;scope=contacts](https://app.hubspot.com/oauth/authorize?client_id=9baffc4b-c9ad-4904-be3c-ea6bc0edc439&amp;redirect_uri=http://localhost&amp;scope=contacts)

**Production Link** : <span style="color: red;">TBD</span>

## Step 2:

Select the portal you want to add the app to from the list provided and allow access.

## Step 3:

You will be redirected to a URL that looks like this:

[http://localhost/?code](http://localhost/?code)=XXX

Copy the value provided for code.

## Step 4:

Send the code to [shyam.sathyanathan@leanswift.com](mailto:shyam.sathyanathan@leanswift.com) to get the app activated in HubSpot. Once the app is activated you should see it listed under &quot;Connected Apps&quot; section. The name of the app should be &quot;LeanSwift HubSpotM3Connector&quot;.

**Note** : This is a temporary procedure until we test the app and release it on the HubSpot Marketplace.

![alt text](C:\Users\tguru\Documents\Markdown\S4.jpg)

## Step 5:

Register a new user account in [https://hubspotm3connectordev.leanswift.com:8081/](https://hubspotm3connectordev.leanswift.com:8081/)

![alt text](C:\Users\tguru\Documents\Markdown\S5_1.jpg)
Click on Register to go to the &#39;Register&#39; page.

Enter your personal details and click on Register.
![alt text](C:\Users\tguru\Documents\Markdown\S5_2.jpg)

## Step 6:

Login using the registered user account from the login page.

Once logged in you will be taken to the home page.

![alt text](C:\Users\tguru\Documents\Markdown\S6.jpg)

Here you can see your user details.

## Step 7:

Click on the configurations tab to update your ION API, HubSpot API and Infor M3 configurations.  
![Step7](C:\Users\tguru\Documents\Markdown\S7.jpg)
Fill up all the fields and click on Update.  
That&#39;s all

## How to find ION API configurations?

1. Login to your Infor OS.
2. Navigate to Infor ION API section
3. Navigate to **Authorized Apps** section from the left pane
4. Locate the backend service if you have already created one. Otherwise you need to create a new one by clicking on the &quot;+&quot; symbol on the top of the page (you need to have security privileges to add an Authorized App in order to do this)
      1. When creating a new service, you have to just provide a name and description for the service. It doesn&#39;t really matter what name and description you provide here.try
5. Once you open the service details, click on the &quot;Download credentials&quot; button.
6. Check the &quot;Create service account&quot; toggle
7. Choose the M3 user with the permissions that you want to allow to the ION API service.
8. Click on download
9. You will get a file with the extension **.ionapi**
10. Open this file in a text editor and fill in the configurations page in HubSpotM3Connector configuration page based on the keys shown on the UI.



## How to find HubSpot portal ID?

Login to your HubSpot portal. Click on the top right &quot;User Account&quot; icon. Portal ID is the number shown below the portal name.


## Important Notes

- ION API needs to be available over the public network. If ION API is not accessible from the AWS server on which the connector application is running, data from HubSpot will not get pushed to M3.
- ION API needs to have a proper SSL certificate issued by a valid Certificate Authority. If not, data will not get pushed to M3.
- A HubSpot portal ID can only be associated with one user account.
- If M3 customer template ID is not configured data will not get pushed to M3.
- Name and Address are mandatory fields and must be available in the company created in HubSpot.If address field is not available at the time of Company creation, address field in M3 will be set as &quot;Address&quot; so that the Copy transaction does not fail.
- HubSpot Response to M3 Request Mapping is as follows:
  - Name - CUNM
  - Street address - CUA1
  - Street address 2 - CUA2
  - City - TOWN
  - Phone number - PHNO
  - Postal code - PONO
- Customer Creation in M3 is done using following API/Transaction
  - CRS610/Copy
  - CUSEXTMI/AddFieldValue
    - FILE - OCUSMA00
    - PK01 - &lt;&lt;M3 CUNO&gt;&gt;
    - PK02 - hs\_companyid
    - A030 - &lt;&lt;hubspot company id&gt;&gt;
