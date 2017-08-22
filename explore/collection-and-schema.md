# Collection And Schema
In this chapter, we will learn how to create a Mongo Collection and attach schema to each Collection. Then, you will master the basic and easy way to store data in your app.

> ❗️Before we dive into the tutorial, we need to make sure we already installed ```aldeed:collection2``` and ```aldeed:autoform``` packages. If you followed the [Package Management]() step by sep, you are good to go.

1. Create `imports/startup/both/collections` directory. This is where we put all Mongo Collection.
2. Create `imports/startup/both/collections/blogs.collection.js` Append:

	```javascript
	Blogs = new Mongo.Collection('blogs');
	```
	> (Optional) We could view our data in the client by installing `meteortoys:allthings`. This is a tool that you can get access to Mongol and JetSetter. Go ahead to play around with it.
	> To get started, run:
	>`$ meteor add meteortoys:allthings`
3. In order to let the file be run in the client side, add in the beginning of `client/main.js` and `server/main.js`:

	```javascript
	// Collections
	import '../imports/startup/both/collections/blogs.collection.js';
	```
4. We want to add schema to our collections in order to use `autoform` package and have all the stuff pre-created for us. (Less pain). So, in the `imports/startup/both/collections/blogs.collection.js`, append:

	```javascript
	import SimpleSchema from 'simpl-schema';
	SimpleSchema.extendOptions(['autoform']);

	Blogs = new Mongo.Collection('blogs');

	BlogSchema = new SimpleSchema({
	    title: {
	        type: String,
	        label: 'Title'
	    },
	    content: {
	        type: String,
	        label: 'Content'
	    },
	    tags: {
	        type: Array,
	        label: 'Tags'
	    },
	    'tags.$': {
	        type: String
	    },
	    author: {
	        type: String,
	        label: 'Author',
	        autoform: {
	            type: 'hidden'
	        },
	        autoValue: function() {
	            return this.userId;
	        }
	    },
	    createdAt: {
	        type: Date,
	        label: 'Created At',
	        autoform: {
	            type: 'hidden'
	        },
	        defaultValue: function() {
	            return new Date();
	        }
	    }
	});

	Blogs.schema = BlogSchema;
	Blogs.attachSchema(BlogSchema);	
	```
5. One last step, we need to attach the schema onto the collection. So, in the `imports/startup/both/collections/blogs.collection.js`, append:

	```javascript
	Blogs.schema = BlogSchema;
	Blogs.attachSchema(BlogSchema);
	```