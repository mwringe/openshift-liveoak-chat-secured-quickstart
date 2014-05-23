#LiveOak Chat QuickStart

This Openshift QuickStart will install the LiveOak Secured Chat example. This example differs from the 'chat' example in that users for this example will have to be authenticated with LiveOak before they can be access the application.

Documentation for the Chat example can be found here:

https://github.com/liveoak-io/liveoak-examples/tree/master/chat/chat-html-secured

#Instruction

To install the quick start from the 'rhc' tool:

```
rhc app create myChatApp diy --from-code git://github.com/liveoak/openshift-liveoak-chat-secured-quickstart
```

or install from the openshift console using the DIY cartridge with the source code option set to git://github.com/liveoak/openshift-liveoak-chat-secured-quickstart 


This example assumes that you have your LiveOak instance running on a gear under your same account called 'liveoak'. If you have your liveoak instance running on another machine, please edit the diy/chat.js.erb file to modify the host and or port to point to the LiveOak instance you want to use.

For example, if your LiveOak is running on a site called 'myAwesomeMBaaS.com' on port 80, you would modify the following line in diy/chat.js.erb from

```
var liveoak = new LiveOak( { host: "liveoak-<%= ENV['OPENSHIFT_NAMESPACE'] %>.<%= ENV['OPENSHIFT_CLOUD_DOMAIN'] %>", port: 8000 } );
```

to 

```
var liveoak = new LiveOak( { host: "myAwesomeMBaaS", port: 80 } );
```

This example also assumes that you have 'chat-html-secured' application setup in your LiveOak instance. The easiest way to do so is to install the LiveOak example quickstart which can be found here: https://github.com/liveoak-io/openshift-liveoak-example-quickstart

Once your liveoak instance has been configured for the chat-html-secured app, you will need to configure a few steps to give your application access to LiveOak. Please start following the instructions at "Create roles for your application" available in the readme here: https://github.com/liveoak-io/liveoak-examples/blob/master/chat/chat-html-secured/README.md
