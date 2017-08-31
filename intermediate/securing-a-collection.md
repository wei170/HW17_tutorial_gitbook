# Securing a Collection

You may found out that when you remove the `insecure` package, you could not post, delete or update a blog any more. The main purpose of `insecure`, and also the `autopublish`, is for faster prototyping. By postponing security considerations until a later stage, these two packages make the browser side just as easy to develop for as the server environment. 

> If you need detailed explaination, visit [this](https://www.discovermeteor.com/blog/meteor-and-security/#insecure-defaults) link


Now let's fix the error and add limitation to the Mongo collections munipulations.

1. In the `imports/startup/both/collections/blogs.collection.js`, append:

	```javascript
	Blogs.allow({
	    insert: function(userId, doc) {
	        // When the user is logged in
	        return !!userId;
	    },
	    update: function(userId, doc) {
	        // When the user is logged in
	        return !!userId;
	    }
	});
	
	Blogs.deny({
	    remove: function() {
	        // We DENY any kind of remove
	        return true;
	    }
	});
	```
	
> Here are two userful tutorial for securing a collection: [The Meteor Chef](https://themeteorchef.com/tutorials/defining-mongodb-collections#tmc-securing-a-collection) and [Discover Meteor](https://www.discovermeteor.com/blog/allow-deny-a-security-primer/)