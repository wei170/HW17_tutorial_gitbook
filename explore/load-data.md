# Load Data
In this chapter, we will learn how to load data on the client using `Blaze Template`. 

> The reason why Meteor use BlazeJs as its default client-side template instead of Angular or React is that Blaze is really easier to understand and more light-weight than other templates. Even though the overall performance cannot be compared with Angular or React, Blaze intuitively helps you to learn Meteor stack better. 

> If you would like to use other client-side templates, go for it. But here, we will stick on Blaze.

1. Create a `client/blogs/blogs.js` file.

	> We will write all js code related to template Blogs, which we will create later, and tempate NewBlog
	
	> Learn more about the `Blaze.js`, go to the [_doc_](http://blazejs.org) page and try more functionalities.
	
	```javascript
	Template.Blogs.helpers({
	    blogs: function() {
	        // Mongodb : find all Blogs
	        return Blogs.find({});
	    }
	});
	```
2. Create a `client/blogs/blogs.html`
3. Append:
	
	```html
	<template name="Blogs">
	    <section class="blogs">
	        {{#each blogs}} 
	            {{> BlogItem}}
	        {{/each}}
	    </section>
	</template>
	
	<template name="BlogItem">
	    <article class="blog">
	        <h3><a href="/blogs/{{_id}}">{{title}}</a></h3>
	        <p>{{content}}</p>
	        <p>
	            <i class="fa fa-tags" aria-hidden="true"></i> 
	            {{#each tag in tags}}
	                {{tag}}
	            {{/each}}
	        </p>
	    </article>
	</template>
	```
	
Now our blog app works as we expected, except that the link of each blog points to no where. So in the next chapter, we will dig into how to get params from a url and use the params to load data.