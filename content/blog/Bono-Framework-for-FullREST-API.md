---
title: Bono Framework for FullREST API
date: 2018-12-14 15:38:36
tags: ['javascript']
cover: 
    src: https://raw.githubusercontent.com/xinix-technology/bono/master/img/bono-logo.png
---

Hello guys, kali ini saya akan membahas tentang menggunakan bono framework, yg menurut saya penggunaan nya lebih mudah dibanding expressjs



> [Bono](https://github.com/reekoheek/node-bono) is light and modular Node.js web application framework (based on Koa.js) to develop api and website.

## Getting Started

```bash
npm i bono
```

setelah itu kita buat satu file dengan nama `index.js`

```javascript
const http = require('http');
const Bundle = require('bono');
const HTTP_PORT = 8888;

let app = new Bundle();

app.use(require('bono/middlewares/json')());

app.get('/', (ctx) => 'hello world');

let server = http.createServer(app.callback());

server.listen(HTTP_PORT, () => console.log(`server listen on port ${HTTP_PORT}`));

```

kemudian jalan kan `node index.js`

buka browser pada alamat [localhost:8888](http://localhost:8888/)

`app adalah Bundle dari keseluruhan index /`

## Create modular Bundle

contoh kita akan membuat bundle dengan endpoint `/api` atau `/auth`

`localhost:8888/api/[params]`

buat file baru dengan nama `api.js`

```javascript
const Bundle = require('bono');

class Api extends Bundle {
  constructor() {
    super();
    this.get('/', this.index.bind(this));
    this.post('/halo', this.halo.bind(this));
    this.get('/user/:idUser', this.getUser.bind(this));
  }
  
  getUser(ctx) {
    return `get id user ${ctx.params.idUser}`;
  }

  halo() {
    return 'Halo api post';
  }

  index(ctx) {
    return 'Hello world from /api';
  }
}

module.exports = new Api();

```

kemudian tambahkan di file `index.js` tadi

```javascript
const api = require('./api');
app.bundle('/api', api);
```

full code

```javascript

const http = require('http');
const Bundle = require('bono');
const HTTP_PORT = 8888;

const api = require('./api');

let app = new Bundle();

app.use(require('bono/middlewares/json')());
app.bundle('/api', api); // <--=-== Here

app.get('/', (ctx) => 'hello world');

let server = http.createServer(app.callback());

server.listen(HTTP_PORT, () => console.log(`server listen on port ${HTTP_PORT}`));

```

eksekusi `node index.js`, buka browser dan arahkan ke endpoint /api/user/2..

untuk method seperti this.get() ada `get()`,`post()`,`put()`,`patch()`,`delete()`


## Middleware
penggunaan middleware, contoh ``memverifikasi user atau memberi authentikasi dengan JWT pada setiap user yg akan mengakses ke endpoint `/api``

buat file `middlewareAuth.js` 

```javascript
const jwt = require('jsonwebtoken');

module.exports = async function(ctx, next) {
  let token = ctx.get('Authorization').split(' ').pop();
  if (!token) {
    ctx.throw(401);
  }

  try {
    let verify = jwt.verify(token, 'secret key');
    ctx.state.user = { ...verify };
  } catch (error) {
    ctx.throw(401);
  }

  await next();
}
```

`ctx.state.user` akan ada selalu di setiap context bundle

setelah itu masukan middleware nya di bundle yg ingin kalian beri authentikasi, pada file index.js

```javascript
const middlewareAuth = require('./middlewareAuth')
api.use(middlewareAuth);
// disini bundle `api` menggunakan authorization
```

selesai deh,

```javascript


const http = require('http');
const Bundle = require('bono');
const middlewareAuth = require('./middlewareAuth')


const HTTP_PORT = 8888;
const api = require('./api');

let app = new Bundle();

app.use(require('bono/middlewares/json')());
api.use(middlewareAuth);

app.bundle('/api', api); // <--=-== Here

app.get('/', (ctx) => 'hello world');

let server = http.createServer(app.callback());

server.listen(HTTP_PORT, () => console.log(`server listen on port ${HTTP_PORT}`));

```

untuk liat full source code DEMO nya bisa langsung liat [DISINI](https://github.com/alfathdirk/node-bono-skeleton)

Sekian dan terimakasih, untuk bertanya2 silahkan komen dibawah


