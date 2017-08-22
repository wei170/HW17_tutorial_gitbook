# Package Management

In this chapter, I will show you where the package file is and how to add and remove a package in Meteor,

Open the `.meteor/packages` file. This is where all your packages are.

Add these packges at the end of this file:

```
kadira:flow-router              # FlowRouter is a very simple router for Meteor.
kadira:blaze-layout             # This is a layout manager designed for Blaze.
erasaur:meteor-lodash           # A wrapper for Lo-Dash (Underscore.js)
stolinski:stylus-multi          # The Level Up Tutorials Stylus/PostCSS Stack.
fortawesome:fontawesome         # Fontawesome
spiderable                      # spiderable is part of Webapp. It's one possible way to allow web search engines to index a Meteor application.
fastclick                       # FastClick is a simple, easy-to-use library for eliminating the 300ms delay between a physical tap and the firing of a click event on mobile browsers.
raix:handlebar-helpers          # Provides a simple way of using sessions and collections in the Meteor Spacebars template environment.
aldeed:collection2-core@2.0.0   # Allows you to attach a schema to a Mongo.Collection. 
aldeed:autoform                 # Adds UI components and helpers to easily create basic forms with automatic insert and update events, and automatic reactive validation.
accounts-ui                     # A turn-key user interface for Meteor Accounts.
accounts-password               # Contains a full system for password-based authentication
matb33:bootstrap-glyphicons     # Bootstrap
zimme:active-route              # This package provide helpers for figuring out if some route or path is or isn't the currently active route.
gwendall:auth-client-callbacks  # Adds client-side onLogin and onLogout callbacks.
```

As long as you save the file, new packages will be automatically added into the app.

Install SimpleSchema NPM package separately (AutoForm 6+), since `autoform` is dependent on this package:

```
$ npm i --save simpl-schema
```