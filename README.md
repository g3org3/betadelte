#HowTo Guide (tlidom_node)

## Index
1. [Installation](https://github.com/g3org3/betadelte/blob/master/README.md#installation)
2. [Post-Install](https://github.com/g3org3/betadelte/blob/master/README.md#post-install)
3. [First Run](https://github.com/g3org3/betadelte/blob/master/README.md#first-time-starting-the-app)
4. [Creating Users](https://github.com/g3org3/betadelte/blob/master/README.md#creating-users)
5. [Make Versions](https://github.com/g3org3/betadelte/blob/master/README.md#how-to-make-tag-versions) 
6. [Super Admin](https://github.com/g3org3/betadelte/blob/master/README.md#update-user-to-super-admin)
7. [Common Issues](https://github.com/g3org3/betadelte/blob/master/README.md#common-issues)

##**Installation**
You need to install the following software in your server:
+ linux distribution [ubuntu, centos, ...]
+ [git](http://git-scm.com)
+ [mongodb](https://www.mongodb.org)
+ [node](https://nodejs.org)
+ [npm](https://nodejs.org)
+ [imagemagick](http://www.imagemagick.org)
+ [librsync and librsync-devel](http://www.howtoinstall.co/en/ubuntu/trusty/main/librsync-dev/) [(rdiff)](https://www.npmjs.com/package/rdiff)

##**Post-Install**

1. Clone repo
	``` sh
	# cd to your destination parent folder
	$ git clone [repo_node]
	$ cd repo_node
	```

2. Copy config base file
	``` sh
	$ cp config/config.base.js config/config.js
	# or
	$ make config
	```

3. Edit config/config.js with your custom configurations.
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
4. Install sails cli
``` sh
	$ sudo npm install -g sails
```
	
**_Optional software to run your app_**
``` sh
$ sudo npm install -g forever
# or
$ sudo npm install -g pm2
```

##**First time starting the app**
1. To start the app just type the following command:
	``` sh
	$ sails lift
	# or
	$ node app.js
	```
> See [common issues](https://github.com/g3org3/betadelte/blob/master/README.md#common-issues) if you have any problems...

2. Go to your favorite web browser and enter your app's server url
	+ example url: `http://192.168.1.29:1337`
	+ initialize the application

		```
		http://192.168.1.29:1337/initialize
		```
	+ Now you're able to interact with the application :D


##**Creating Users**
To create a user you need to run an api call **user_register**
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

##**Update user to super admin**
``` javascript
db.users.update(
	{ _id: ObjectId("ID") },
	{
		// userinfo ...
		userType: 'sa'	
	});
```

##**How to make tag versions**
 Before commiting changes!
 	+ modify config.base.js
 		```
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

##Common Issues
+ First install may cause error because the db does'nt exit, just lift again your app with:
	`$ sails lift`

+ Trying tu lift at port :80 with no root user will fail, try with sudo instead:
	`$ sudo sails lift`

+ lkasdflkajsfd
