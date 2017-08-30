# Publish and Subscribe

In this chapter, we will learn how to publish data from the server and subscribe them on the client. Since `autopublish` and `insecure` packages are not safe in producation and munipulating data in the client will give the browser too much burden.

1. Delete `autopublish` and `insecure` in the `.meteor/packages`
2. Create a `imports/api/blogs/publish.js` file
3. Append:

	```
	Meteor.publish('blogs', () => {
   		return Blogs.find({});
	});
	```
4. In the beginning of `client/blogs/blogs.js`, append:

	```
	// Subscribe blogs
	Meteor.subscribe('blogs');
	```
	
> After delete the `insecure` package, you will find that you cannot post a new blog anymore, and there is no error message in both client side and server side.
> 
> Because the meteor does not let you to post if you do not tell the Mongo.Collection to accept `insert`, `update`, or `delete`.
> 
> In the next chapter, we will fix this problem and explain the whole `insert` process in Meteor.