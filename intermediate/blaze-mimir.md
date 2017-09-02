# Blaze Mímir

This chapter we will take a deeper look into the Blaze template. We will learn how to use 

* `{% raw %}{{# if}}{% endraw %}`
* `{% raw %}{{# each comments}}{% endraw %}`
* `{% raw %}{{{> html}}}{% endraw %}`
* `Templates.events({})`
* `Templates.helpers({})`
* `Templates.onCreated(function() {})`
* `TemplateInstance#subscribe()`
* `TemplateInstance#autorun()`
* `ReactiveVar` in `zimme:active-route` package
* Pass data to a template

We will add `Comments` collections to each blog, allow authors to change the their blogs and enable the page change reactively.

### Comments
1. Create a `imports/startup/both/collections/comments.collection.js`, and append:

	```javascript
	import SimpleSchema from 'simpl-schema';
	SimpleSchema.extendOptions(['autoform']);
	
	Comments = new Mongo.Collection('comments');
	
	CommentsSchema = new SimpleSchema({
	    blogId: {
	        type: String,
	        autoform: {
	            type: 'hidden'
	        }
	    },
	    createdBy: {
	        type: String,
	        autoValue: function() {
	            return this.userId;
	        },
	        autoform: {
	            type: 'hidden'
	        }
	    },
	    content: {
	        type: String
	    },
	    createdAt: {
	        type: Date,
	        autoValue: function() {
	            return new Date();
	        },
	        autoform: {
	            type: 'hidden'
	        }
	    }
	});
	
	Comments.schema = CommentsSchema;
	Comments.attachSchema(CommentsSchema);
	
	Comments.allow({
	    insert: function(userId, doc) {
	        return !!userId;
	    }
	});
	```
	
2. In both `client/main.js` and `server/main.js`, add:
	
	```javascript
	import '../imports/startup/both/collections/comments.collection.js';
	```

### Add Comments Template

1. Create a `client/comments` directory, a `client/comments/comments.html`, and a `client/comments/comments.js`.
2. In the `client/comments/comments.html`, append:

	```html
	{% raw %}
	<template name="Comments">
	    <section class="comment">
	        <h3>Comments</h3>
	        {{#each comment in comments}}
	            {{#if isAuthor comment.createdBy}}
	                <section class="comment-right">
	                    <h3>Test Right</h3>
	                    <p>{{{comment.content}}}</p>
	                </section>
	            {{else}}
	                <section class="comment-left">
	                    <h3>Test Left</h3>
	                    <p>{{{comment.content}}}</p>
	                </section>
	            {{/if}}
	        {{/each}}
	    </section>
	    <br>
	    {{> NewBlogComment blogId=blogId}}
	</template>

	<template name="NewBlogComment">
	    <section class="new-comment-container">
	        {{#autoForm collection="Comments" id="insertBlogCommentForm" type="insert"}}
	            <section>
	                <h3>Post A Comment</h3>
	                {{> afQuickField name='blogId' value=blogId}}
	                {{> afQuickField name='content' rows=3}}
	            </section>
	            <button type="submit" class="btn">Submit</button>
	        {{/autoForm}}
	    </section>
	</template>
	{% endraw %}
	```
3. In the `client/comments/comments.js`, append:

	```javascript
	Template.Comments.onCreated(function() {
	    // `this` is a TemplateInstance
	    var self = this;
	
	    // use a reactivevar to store if the author is editing
	    self.isEditing = new ReactiveVar(false);
	
	    // Subscribe comments only in this template
	    var subs = self.subscribe('comments', self.data.blogId);
	
	    self.autorun(function() {
	        if (!subs.ready()) return;
	
	        // Add anything below you want that subs has changed
	
	    });
	});
	
	Template.Comments.helpers({
	    'blogId': () => {
	        return Template.instance().data.blogId;
	    },
	    'comments': () => {
	        return Comments.find({});
	    },
	    'isAuthor': (authorId) => {
	        return Meteor.userId() === authorId;
	    }
	});
	
	Template.NewBlogComment.helpers({
	    'blogId': () => {
	        return Template.instance().data.blogId;
	    }
	});
	```
4. Now we need to publish all Comments related to a blog. Create `imports/api/comments/publish.js`, and append:

	```javascript
	Meteor.publish('comments', (blogId) => {
	    return Comments.find({blogId: blogId});
	});
	```	
5. In the `server/main.js`, append:

	```javascript
	import '../imports/api/comments/publish.js';
	```
