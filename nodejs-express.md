# nodejs express

_Status: Published_
_Created: 2017-01-05 03:19:40_
_Tags: javascript_

<code>
npm init

npm install express --save
npm install body-parser --save
npm install nodemon --save / --g
npm install bcryptjs --save

</code>

create app.js
<code>
var express = require('express');
var bodyParser = require('body-parser');
var app = express();

app.get('/', function (req, res) {
  res.send('Hello World!')
})

app.listen(3000, function () {
  console.log('listening on port 3000')
})

</code>