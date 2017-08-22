#Layouts
In this chapter, we will use `Template` in `Blaze`, and `FlowRouter` to build our basic `HomeLayout`, which is a static page, and `MainLayout`, which is a dynamic rendering page.

### HomeLayout

1. In the `client/` directory, create `layouts/` directory to store all layouts.
2. Create a `client/layouts/HomeLayout.html` file, and append:

	```html
	<template name="HomeLayout">
		<header>
			<h1>Hello From HomeLayout</h1>
			{{> loginButtons}}
		</header>
	</template>
	```
	> `{{> loginButtons}}` is the way to implement a template by `{{> template_name}}`.
	> Since we are using `accounts-ui` package, we can simply use `loginButtons` template here to handle authentication in our app. We will dig deeper into it later.
3. Create a `imports/startup/lib/` directory to put our `routes.js` inside of it.
4. In the `imports/startup/lib/routes.js`, append:

	```javascript
	FlowRouter.route('/', {
	    name: 'home',
	    action() {
	        BlazeLayout.render('HomeLayout');
	    }
	});
	```

### MainLayout

1. Create a `client/layouts/MainLayout.html` file, and append:

	```html
	<template name="MainLayout">
	    <header>
	        <h1>Blog App</h1>
	        {{> loginButtons}}
	    </header>
	    <main>
	        {{> Template.dynamic template=main}}
	    </main>
	</template>

	<template name="Test">
	    <h3>TEST!!!</h3>
	</template>
	```
	>  `{{> Template.dynamic template=main}}` is how dynamic page to render other templates inside of it. We need to tell the `FlowRouter`.

2. In the `imports/startup/lib/routes.js`, append:

	```javascript
	FlowRouter.route('/test', {
	    name: 'test',
	    action() {
	        BlazeLayout.render('MainLayout', {main: 'Test'});
	    }
	});
	```
	> `BlazeLayout.render('MainLayout', {main: 'Test'});` is how we tell the `FlowRouter` which template we insert into the `MainLayout` dynamic page
