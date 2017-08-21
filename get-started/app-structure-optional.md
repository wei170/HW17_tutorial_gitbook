# App Structure (Optional)
Meteor has its own _recommended_ code structure, and directoriese and files names.

```imports/```: ALL application code
> Meteor will load all files outside of any directory named ```imports/``` in the application using the [default load order rules](https://guide.meteor.com/structure.html#load-order).

```client/main.js``` and ```server/main.js```: Two eagerly loaded files
> In order to define explicit entry points for both the client and the server.

>> Meteor will ensure that any file in any directory named ```server/``` will only be available on the server, and ```client/``` be on the client.

Let's take a look at the [Todos example app](https://www.meteor.com/tutorials/blaze/creating-an-app), the official Meteor 'helloworld' application. It is a great example to follow when structuring your app.

```
imports/
  startup/
    client/
      index.js                 # import client startup through a single index entry point
      routes.js                # set up all routes in the app
      useraccounts-configuration.js # configure login templates
    server/
      fixtures.js              # fill the DB with example data on startup
      index.js                 # import server startup through a single index entry point
  api/
    lists/                     # a unit of domain logic
      server/
        publications.js        # all list-related publications
        publications.tests.js  # tests for the list publications
      lists.js                 # definition of the Lists collection
      lists.tests.js           # tests for the behavior of that collection
      methods.js               # methods related to lists
      methods.tests.js         # tests for those methods
  ui/
    components/                # all reusable components in the application
                               # can be split by domain if there are many
    layouts/                   # wrapper components for behaviour and visuals
    pages/                     # entry points for rendering used by the router
client/
  main.js                      # client entry point, imports all client code
server/
  main.js                      # server entry point, imports all server code
```

###Default file load order
1. HTML template files are **always** loaded first
2. Files beginning with ```main.``` are loaded **last**
3. Files inside **any** ```lib/``` directory are loaded next
4. Files with deeper paths are loaded next
5. Files are then loaded in alphabetical order

### Special directories

```
imports/
node_modules/
client/
server/
public/
private/
client/compatibility
tests/
```