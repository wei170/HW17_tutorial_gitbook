# Auth Client Callbacks

Right now, when a user log in, they will not be redirected to the `blogs` page. Or when a user log out, they will also not be redirected to the `home` page. So in this chapter, we will learn how to do this trick.

> `gwendall:auth-client-callbacks` package do the work.

1. In the `imports/startup/lib/routes.js`, append:

	```javascript
	// Login/Logout trigger
	if (Meteor.isClient) {
	    Accounts.onLogin(function() {
	        FlowRouter.go('blogs');
	    });
	
	    Accounts.onLogout(function() {
	        FlowRouter.go('home');
	    });
	}
	
	FlowRouter.triggers.enter([function() {
	    if (!Meteor.userId()) {
	        FlowRouter.go('home');
	    }
	}]);
	```
2. Also in the `imports/startup/lib/routes.js`, in the `action` function of the FlowRouter which named `home`, add the following before `BlazeLayout.render('HomeLayout');`

	```
    if (Meteor.userId()) {
        FlowRouter.go('blogs');
    }
	```