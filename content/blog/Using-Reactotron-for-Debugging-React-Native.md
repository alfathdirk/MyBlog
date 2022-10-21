---
title: Using Reactotron for Debugging React Native
date: 2018-12-20 19:35:38
tags: ['javascript', 'react native']
cover: 
    src: https://i.ytimg.com/vi/tPBRfxswDjA/maxresdefault.jpg
---

Hi gais, kali ini gw mau bahas tools debuging ReactNative, tadi abis nyari tools debug, sebenernya ada banyak banget tapi gua nyoba salah satu nya, yaitu reactotron

![reactotron](https://github.com/infinitered/reactotron/raw/master/docs/images/readme/reactotron-demo-app.gif)

untuk mac install nya tinggal pake brew

```bash
$ brew cask install reactotron
$ npm i reactotron-react-native --save-dev # di project RN ya
```

buka apps nya

kemudian masuk ke project react native kalian, bikin satu file `debugger.js`

paste code ini ke file tersebut

```js
import Reactotron from 'reactotron-react-native'

Reactotron
  .configure() // controls connection & communication settings
  .useReactNative() // add all built-in react native plugins
  .connect() // let's connect!

export default ReactLogger = Reactotron; // ReactLogger will be global variable
```

kemudian panggil file debugger.js di `index.android.js` or `app.js`

```js
import './src/middleware/debugger';
```

kemudian `npm start`

setelah itu coba panggil di `render()`

```js
ReactLogger.log('hello rendering world');
```

akan muncul deh di reactotron ..

silakan ulik2 sendiri, untuk dokumentasi nya bisa liat langsung [disini](https://github.com/infinitered/reactotron)

Sekian dan Happy Coding !!