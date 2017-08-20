# Clean Up
In this tutorial, we will clean up default scaffolding codes and create directories and files for our future usage.

1. In the ```client/```, remove ```main.css``` and ```main.html```. 

	> Since we will code our app in the recommending structure, all ```.html``` and ```.js``` will be in the ```imports/ui/*```
2. Clean up the ```main.js``` and insert:

	```
	import { Meteor } from 'meteor/meteor';

	Meteor.startup(() => {
  	// code to run on server at startup
	});

	```
3. Create ```imports/``` directory in the root.
4. Create ```imports/startup/```, ```imports/api/```, and ```imports/ui/``` directories.
5. Create ```imports/startup/server``` and ```imports/startup/client``` directories.