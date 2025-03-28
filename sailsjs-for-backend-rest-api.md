# Sailsjs for backend rest api

_Status: Published_
_Created: 2016-03-30 04:07:56_
_Tags: javascript, sailsjs_

==
help with salsas:
<ul>
<li>Google Groups: sails.js</li>
<li>IRC: #sailsjs</li>
<li>Stack Overflow (using tag sails.js)</li>
</ul>
==
instal

mac:
nodejs.org
download pkg
(
/usr/local/bin/node
/usr/local/bin/npm
add to $PATH
/usr/local/bin
)

(sudo) npm install sails â€“global

==
setup first project
<b>sails new firstApp<b>

move to folder
cd firstApp

to start sails:
<b>sails lift</b>

generate new model via blueprint engine
<b>sails generate api user</b>

then question about migrate on sails lift
choose alter in non Prod env
change firstApp/config/model.js
<code>
module.exports.models = {
migrate: 'alter'
};
</code>
http://localhost:1337/user
first results
 in json response []

localhost:1337/user/create?name=HJSnips
results in
<code>
[
  
  {
    "name": "HJSnips",
    "createdAt": "2016-03-30T07:30:39.555Z",
    "updatedAt": "2016-03-30T07:30:39.555Z",
    "id": 1
  }
]
</code>
==
use Sails built-in integration
with websockets and Socket.io

create
firstApp/assets/js/test.js
<code>
io.socket.get('/user', function (users){ console.log(users);});
io.socket.on('user', function (message) {
console.log("Got message: ", message);
});
</code>
==
policies
firstApp/config/policies.js
<code>
module.exports.policies = {
'UserController': {
'create': ['sessionAuth']
}
};
</code>

==
static assets
<b>npm install sails-generate-static --save</b>

<b>sails generate static</b>

sails lift
now when adding content to assets Grunt will create routes files in .tmp

== css assets
to use css in html via grunt make sure:
<b>
&lt;!--STYLES--&gt;<br/>&lt;!--STYLES END--&gt;<br/>
are in!
</b>
<code>
<head>
	<title>New Sails App</title>
	<!-- Viewport mobile tag for sensible mobile support -->
	<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
    
<!--STYLES-->
<!--STYLES END-->
</head>
</code>
<code>
 <html>
 <body>
 <!--STYLES--> 
 <!--STYLES END-->
 </head>
 <body>
 <!--TEMPLATES-->
 <!--TEMPLATES END-->
 <!--SCRIPTS-->
 <!--SCRIPTS END-->
 </body>


 </html>
</code>