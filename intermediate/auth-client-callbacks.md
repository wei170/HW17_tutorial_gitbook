# Auth Client Callbacks

Right now, when a user log in, they will not be redirected to the `blogs` page. Or when a user log out, they will also not be redirected to the `home` page. So in this chapter, we will learn how to do this trick.

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