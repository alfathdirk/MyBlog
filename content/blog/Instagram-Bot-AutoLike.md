---
title: Instagram Bot AutoLike
date: 2018-12-12 00:19:29
tags: ['bot', 'javascript']
cover: 
    src: https://cmkt-image-prd.global.ssl.fastly.net/0.1.0/ps/1961026/1360/906/m1/fpnw/wm1/cbpmvzimvpjuzdf6inyhz1yqwuqqfzpzj0lrn0fmixcgevjgeldddgkqw5ldpj9j-.jpg?1480412871&s=9e916a42203d79b0c7c7c54281aceaf1
---

Udah lama ga nge blog, dan nyoba themes baru hexo
## Bot like instagram
perlu diketahui `CODE INI BUKAN BUAT DAPETIN LIKE BANYAK` 

`This code for like your timeline friends photo/video automatically`

pertama install alexis
```bash
npm i alexis
```

bikin file baru namain `index.js`

kemudian paste code ini ke file `index.js` tadi yang baru dibuat

```javascript
const Ig = require('alexis');
let ig = new Ig();

const TIMEOUT = 6000; // 6 seconds;

const username = 'username'; // ganti sama username dan password kalian
const password = 'password';

async function doLike () {
  try {
    await ig.login(username, password);
    let medias = await ig.getTimeLineFeed();
    medias.map(async ({ node }) => {
      let now = new Date().getTime();
      let fourHours = 3600 * 4 * 1000;
      let mediaTimePost = node.taken_at_timestamp * 1000;
      if (mediaTimePost >= now - fourHours) {
        if (!node.viewer_has_liked) {
          await ig.like(node.id);
        }
      }
    });
  } catch (error) {
    console.error(error);
  }
  setTimeout(doLike, TIMEOUT);
}

doLike();
```

kemudian save, dan jalan kan

```bash
node index.js
```

selesai deh..

mudah bukan???
comment dibawah jika kalian punya ide atau pertanyaan kripik dan kentang :D