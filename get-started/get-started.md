#Get Started

In this tutorial, we are going to create a blog app to manage blog and comment posting, authentication checking, and the implementation of some third-party plugins. By the end, you should have a comprehensive understanding of meteor and its project structure.

To create the app, open your terminal and type:

`meteor create blog-app`

This will create a new folder called `blog-app` with all of the files that a Meteor app needs:

```
client/main.js # a JavaScript entry point loaded on the client
client/main.html # an HTML file that defines view templates
client/main.css # a CSS file to define your app's styles
server/main.js # a JavaScript entry point loaded on the server
package.json # a control file for installing NPM packages
.meteor # internal Meteor files
.gitignore # a control file for git
```

To run the newly created app:

```
cd simple-todos
meteor
```

Open a web browser and go to `http://localhost:3000` to see the app running.