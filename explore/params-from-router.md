# Get Params From Router
In this chapter, we will learn how to get the params from the router. For example, we set the url pattern as `blogs/:id` and the url is `blogs/3G5c7obGmds9J7j6T`. We need to know a way to get the `:id` data.

At first, we create a html template to show all information, assuming that we already get the `:id` param and use it to find the right blog.

1. In the `imports/startup/lib/routes.js`, append:

	```javascript
	FlowRouter.route('/blogs/:id', {
	    name: 'blog',
	    action() {
	        BlazeLayout.render('MainLayout', {main: 'Blog'});
	    }
	});
	```
2. Create a `client/blogs/blog.html` file.
	> This is the html template for a single blog
3. Append:

	```html
	<template name="Blog">
	    {{#with blog}}
	        <section class="blog">
	            <h3><a href="/blogs/{{_id}}">{{title}}</a></h3>
	            <p>{{content}}</p>
	            <p>
	                <i class="fa fa-tags" aria-hidden="true"></i> 
	                {{#each tag in tags}}
	                    {{tag}}
	                {{/each}}
	            </p>
	        </section>
	    {{/with}}
	</template>
	```
	> Check [here](http://blazejs.org/api/blaze.html#Blaze-With) to know how to use `#with`
	> `blog` is the blog object data we want

Then, we need to update `client/blogs/blogs.js` file, or create a new js file to handle this, to grap the `:id` param and find the exact blog.

*  Append:

	```
	Template.Blog.helpers({
	    blog: function() {
	        return Blogs.findOne({_id: FlowRouter.getParam('id')});
	    }
	});
	```
	
Now, each blog has a corresponding page.

## Foreword
In the next section, we will go to the intermediate part. We will learn how to add authentication guard, how to redirect after login and logout, how to use third party oauth auth, what is pub/sub, what is `Meteor.method` and etc.
> My suggestion to learn Meteor and any other framework, no matter it is client-side or server-side, go to read blogs and watch related tech-talks to boost your knowledge. 

> Only stick on the official documentation without any practice is a disaster. Attending hackathons is the best idea to apply your knowledge into a real-world-like developing enviornment.