---
title: Scraping tokopedia with Luwak
date: 2018-12-12 10:06:39
tags:
cover: 
    src: https://ak9.picdn.net/shutterstock/videos/17372809/thumb/1.jpg
---

Kali ini bahasan kita adalah scraping atau mengambil data tokopedia, bukan hacking tapi mengambil konten2 yg dapat diakses oleh semua pihak dengan memilih konten yg diperlukan untuk di tampilkan di situs milik kita

### Install Luwak
Luwak disini bukan white coffee yg aman dilambung ga bikin kembung, tapi tools untuk melakukan scrapping, yg setiap data web DOM akan langsung diolah menjadi bentuk `JSON`, amazing bukan tools satu ini, oke langsung aja masuk console/terminal kalian

```bash
npm install luwak
```

## Write File
Kemudian bikin file `index.js`

disini kita akan mengambil konten flash sale
```javascript
const url = 'http://ace.tokopedia.com/hoth/discovery/render/component/desktop/flash-sale/62532?rpc_Page=1&rpc_ResultPerPage=20';
let data = await luwak(url)
      .filter('hitung', function (value) {
        let newString = value.replace('200-square', '700')
        return newString;
      })
      .select([{
          '$root': '.td_col__5',
          judul: 'h1',
          priceAfter: '.price-after',
          priceBefore: '.price-before',
          image: 'img@src | hitung',
          link: 'a@href'
      }])
      .fetch();
```

`$root` = adalah inti dari tag html yg ingin kalian ambil content nya *(required use)

`judul` = adalah penamaan object json untuk text yg berada di h1 contoh `<h1>anu</h1>` , akan menampilkan anu

dan seterusnya..
method `.filter()` berfungsi untuk mengevaluasi return value.

## Execute Code
Saatnya eksekusi code nya

```bash
node index.js
```

ouputnya akan seperti ini

```json
[ { judul: 'SOUL UPBEAT High Performance Earphones - Hitam',
    priceAfter: 'Rp 121.212',
    priceBefore: 'Rp 224.850',
    image:
     'https://ecs7.tokopedia.net/img/cache/700/product-1/2018/11/27/21256362/21256362_d447a784-2cdf-48fa-af7e-491119482336_800_800.jpg',
    link:
     'https://www.tokopedia.com/soulofficial/soul-upbeat-high-performance-earphones-hitam?trkid=f%3DP0Cb0_src%3Dsprint-sale_page%3D1_ob%3D17_catid%3D565' },
  { judul: 'Vaneli Crystal 134 gr FS',
    priceAfter: 'Rp 12.750',
    priceBefore: 'Rp 15.000',
    image:
     'https://ecs7.tokopedia.net/img/cache/700/product-1/2017/10/9/22998910/22998910_711e7a8c-896d-4ff2-8d44-3450da23568f_576_576.jpg',
......

```
mudah bukan??
ini adalah contoh dengan method basic, Luwak ini dapat menggunakan middleware engine, contoh seperti `nightmare`, dsb

penggunaan engine biasanya dipakai jika web tidak bisa discrap menggunakan basic seperti ini, untuk lebih lengkap contoh penggunaan middleware engine luwak bisa lihat [disini](https://github.com/xinix-technology/luwak/tree/master/examples).


Thanks to [reekoheek](https://github.com/reekoheek), buat tools keren nya !!