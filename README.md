# Guide - tilidom_node [![version](https://img.shields.io/badge/version-v0.2.6-brightgreen.svg?style=flat)]()

## Index
1. [Installation](https://github.com/g3org3/betadelte/blob/master/README.md#installation)
2. [Post-Install](https://github.com/g3org3/betadelte/blob/master/README.md#post-install-)
3. [First Run](https://github.com/g3org3/betadelte/blob/master/README.md#first-time-starting-the-app-)
4. [Creating Users](https://github.com/g3org3/betadelte/blob/master/README.md#creating-users-)
5. [Super Admin](https://github.com/g3org3/betadelte/blob/master/README.md#update-user-to-super-admin-)
6. [Make Versions](https://github.com/g3org3/betadelte/blob/master/README.md#how-to-make-tag-versions-) 
7. [Common Issues](https://github.com/g3org3/betadelte/blob/master/README.md#common-issues-)

##**Installation**
You need to install the following software in your server:
+ linux distribution [ubuntu, centos, ...]
+ [git](http://git-scm.com)
+ [mongodb](https://www.mongodb.org)
+ [node](https://nodejs.org)
+ [npm](https://nodejs.org)
+ [imagemagick](http://www.imagemagick.org)
+ [librsync and librsync-devel](http://www.howtoinstall.co/en/ubuntu/trusty/main/librsync-dev/) [(rdiff)](https://www.npmjs.com/package/rdiff)

##**Post-Install** [^](https://github.com/g3org3/betadelte/blob/master/README.md#index)

1. Clone repo

	``` sh
	# cd to your destination parent folder
	$ git clone tilidom_node.git
	$ cd tilidom_node
	```
2. Install npm modules
	``` sh
	$ sudo npm install
	```

3. Copy config base file
	``` sh
	$ cp config/config.base.js config/config.js
	# or
	$ make config
	```

4. Edit config/config.js with your custom configurations.
	+ change host to server's ip
	+ change db name
	+ change port
	``` javascript
	// config/config.js
	{
		mongo: {
			database: 'sampleDb' // <- desire dbname 
		},
		local: {
			port: 1337,           // <- desire port
			host: '192.168.1.100' // <- server's ip
		}
	}
	```
5. Install sails cli
``` sh
	$ sudo npm install -g sails
```
	
**_Optional software to run your app_**
``` sh
$ sudo npm install -g forever
# or
$ sudo npm install -g pm2
```

##**First time starting the app** [^](https://github.com/g3org3/betadelte/blob/master/README.md#index)
1. To start the app just type the following command:
	``` sh
	$ sails lift
	# or
	$ node app.js
	```
> See [common issues](https://github.com/g3org3/betadelte/blob/master/README.md#common-issues-) if you have any problems...

2. Go to your favorite web browser and enter your app's server url
	+ Example url: `http://192.168.1.29:1337`
	+ Initialize the application

		```
		http://192.168.1.29:1337/initialize
		```
	+ You've finished installing the app :D


##**Creating Users** [^](https://github.com/g3org3/betadelte/blob/master/README.md#index)
To create a user you need to run an api call **user_register**
> Request

``` javascript
	// example params
	params: {
		username: 'example@domain.com',
		password: 'pass1234',
		accept_terms: 1
	}
	
	// make request
	GET /tilidom/tilidrive-api/user_register
```
> Response

``` javascript
{
    "message": "User was successfully registered",
    "code": 0
}
```

##**Update user to super admin** [^](https://github.com/g3org3/betadelte/blob/master/README.md#index)
``` javascript
db.users.update(
	{ _id: ObjectId("ID") },
	{
		// userinfo ...
		userType: 'sa'	
	});
```

##**How to make tag versions** [^](https://github.com/g3org3/betadelte/blob/master/README.md#index)
Before commiting changes!
+ modify config.base.js

	```javascript
	version: {
		current		: 'v0.2.6', // <= change version
		description	: 'bug fix: profile image', // <= change description of new version
		log		: 'logs/version.log'
	},
	```
```sh
 # commit changes
 $ commit -m "my commit"
 
 # create tag
 $ make tag
 
 # push changes
 $ git push -u origin master --tags
```

##Common Issues [^](https://github.com/g3org3/betadelte/blob/master/README.md#index)
+ The first time you start your app could crash, because no db was created before. Start again the application and there should not be an error.
	`$ sails lift`

+ Trying start the app at port :80 getting errors?
	+ you need more priveliges to start your app
	`$ sudo sails lift`

+ more soon
