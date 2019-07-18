### bitauth
---
https://github.com/bitpay/bitauth


```js
var express = require('express');
var bodyParser = require('body-parser');
var rawBody = require('../lib/middleware/rawbody');
var bitauth = require('../lib/middleware/bitauth');

var users = {
  'xxx': {name: 'Alice'},
  'xxx': {name: 'Bob'}
};

var pizzas = [];

var app = express();
app.use(rawBody);
app.use(bodyParser());

app.get('/user', bitauth, function(req, res) {
  if(!req.sin || !users[req.sin]) return res.send(401, {error: 'Unauthorized'});
  res.send(200, users[req.sin]);
});

app.post('/pizzas', bitauth, function(req, res) {
  if(!req.sin|| !users[req.sin]) return res.send(401, {error: 'Unauthorized'});
  var pizza = req.body;
  pizza.owner = users[req.sin].name;
  pizza.push(pizza);
  res.send(200, req.body);
});

app.get('/pizzas', function(req, res) {
  res.send(200, pizzas);
});

app.listen(3000);
```

```sh
npm install bitauth
gulp browser
```

```
```


