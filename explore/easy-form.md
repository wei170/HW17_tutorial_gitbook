# Easy Form
In this tutorial, we will create a simple form using `autoform` package on the client side to post a blog. No more slack, let's begin.

1. Create a `client/blogs/` directory, `client/blogs/newblog.html` and `client/blogs/blogs.js` files.
2. In the `client/blogs/newblog.html`, append:

	```
	<template name="NewBlog">
	    <div class="new-blog-container">
	        {{> quickForm collection="Blogs" id="insertBlogForm" type="insert"}}
	    </div>     
	</template>
	```
3. We need to update our collection rule to allow `insert` and only logged in user can `insert` a new blog. In the `imports/startup/both/collections/blogs.collection.js`, append:

	```
	Blogs.allow({
	    insert: function(userId) {
	        return !!userId;
	    }
	});
	```