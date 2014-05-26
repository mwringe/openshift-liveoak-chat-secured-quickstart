#LiveOak Secured Chat Example QuickStart

This OpenShift QuickStart will create and configure a DIY gear to host the LiveOak Secured Chat example's HTML 5 client side code. It will requires access to a LiveOak instance already configured for the chat example's backend logic.

For more information on how to configure a LiveOak gear in OpenShift with the example's backend already configured, please refer to the following quickstart:

https://github.com/liveoak-io/openshift-liveoak-examples-quickstart

Or refer it its application.json file available [here] (TODO: insert link here)

The Secured Chat example differs from the normal chat example in that some of the chats are now secured to specific users. Owners of chats will be able to delete and manage their own chats.

If you wish to run the Secured Chat example locally on your own machine, please see the  example available here:

https://github.com/liveoak-io/liveoak-examples/tree/master/chat/chat-html-secured

#Installing the Secured Chat Client Example

To install the quick start from the 'rhc' tool:

```
rhc app create mySecuredChatApp diy --from-code git://github.com/liveoak/openshift-liveoak-client-chat-secured-quickstart
```

or install from the OpenShift console using the DIY cartridge with the source code option set to git://github.com/liveoak/openshift-liveoak-client-chat-secured-quickstart 


This example assumes that you have your LiveOak instance running on a gear under your same account called 'liveoak'. If you have your liveoak instance running on another machine, please edit the diy/chat.js.erb file to modify the host and or port to point to the LiveOak instance you want to use.

For example, if your LiveOak is running on a site called 'myAwesomeMBaaS.com' on port 80, you would modify the following line in diy/chat.js.erb from

```
var liveoak = new LiveOak( { host: "liveoak-<%= ENV['OPENSHIFT_NAMESPACE'] %>.<%= ENV['OPENSHIFT_CLOUD_DOMAIN'] %>", port: 8000 } );
```

to 

```
var liveoak = new LiveOak( { host: "myAwesomeMBaaS", port: 80 } );
```

#Configuring the Secured Chat Client Example

The following steps assume that your liveoak instance is running on a gear in OpenShift with a url like http://liveoak-USERNAME.rhcloud.com, you will need to adapt the urls listed to your own specific environment.

The following steps also assume that your secured chat gear is available at a url like http://securedchat-USERNAME.rhcloud.com, you will need to adapt the urls listed to your own specific environment.

A few more steps will need to be completed before you can run the Secured Chat example. You will need to authorizing your gear for use in LiveOak.

1. Create roles for your application (Manual step required)
  * login to the admin console at http://liveoak-USERNAME.rhcloud.com/admin#/applications/chat-html-secured/application-settings
  * add 2 new roles "admin" and "user". 
  * select "user" to be default role 
  * click "Save"

3. Add an HTML client for your Secured Chat Gear
  * login to the admin console at http://liveoak-USERNAME.rhcloud.com/admin#/applications/chat-html-secured/application-clients
  * click 'add client' and fill in the following values:
    * Name: "chat-html-secured-client"
    * Platform: HTML-5
    * Redirect URI: "http://securedchat-USERNAME.rhcloud.com/*" (click button "Add")
    * Web Origins: "http://securedchat-USERNAME.rhcloud.com" (click button "Add")
    * Scope: select both "admin" and "user" scopes
  * click 'save'


#Accessing the Secured Chat Client

After you your gear has been created, you should be presented with a link to access the website. The first time you access this page it may ask you to login as a user. To create a new user, please click on the 'register' link. Alternatively, you can also manage your users through the KeyCloak admin console, which is available at http://liveoak-USERNAME.rhcloud.com/auth/admin

After logging in, the website will take you to the secured chat example, which allows you to login to send and receive chats in real time. Note that anyone can register to login to this application and all chats and correspondence should be considered public.
