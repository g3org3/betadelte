#HowTo Guide (tlidom_node)
___
## Index
---
###**Installation**
You need to install the following software in your server:
--- linux distribution
--- git
--- mongodb
--- node
--- npm
--- imagemagick
--- librsync and librsync-devel (rdiff)

___
####**Post-Install**

1. Clone repo
	```
	$ git clone [repo_node]
	```

2. Copy config base file
	```
	$ cd [repo_node]
	$ cp config/config.base.js config/config.js
	```

3. Edit config/config.js with your custom configurations
example actions:
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

	```
		$ sudo npm install -g sails
	```
	
**--------- Optional Install ---------**
```
$ sudo npm install -g forever
```
```
$ sudo npm install -g pm2
```
---
####**--- First time lifting app ---**
1. To lift your app just enter the commando below:

	```
	$ sails lift
	```
See subtopic common issues if you have any problems...

2. Go to your favorite web browser to your server's url
	e.g. > `http://192.168.1.100:1337`
	+ initialize the application
		e.g. `http://HOST:PORT/initialize`
	+ Now you're able to interact with the application :D

---
####**--- Creating Users ---**
To create a user you need to run an api call **user_register**
e.g.
``` javascript
	params: {
		username: 'example@domain.com',
		password: 'pass1234',
		accept_terms: 1
	}
	GET /tilidom/tilidrive-api/user_register
```
response
``` javascript
{
    "message": "User was successfully registered",
    "code": 0
}
```


---
###Common Issues
+ First install may cause error because the db does'nt exit, just lift again your app with:
	`$ sails lift`

+ Trying tu lift at port :80 with no root user will fail, try with sudo instead:
	`$ sudo sails lift`

+ lkasdflkajsfd