---
title: AXEL alternative IDM for Linux/Mac
date: 2018-12-14 00:14:30
tags: ['linux', 'tutorial']
cover: 
    src: https://alfathdirk.files.wordpress.com/2015/06/axel.png
---

Axel is A light download accelerator for Linux.
tapi axel ini berbentuk CLI / Command Line Interface..

Nah Tujuan utamanya adalah bisa download , teserah lu mau download apaan aja ..
Contoh gua mau download lagu dari link ini http://imondepression.com/sotd/mae%20-%20suspension.mp3

tinggal tulis
```bash
axel -v -a -n8 http://imondepression.com/sotd/mae%20-%20suspension.mp3
```

![image](https://alfathdirk.files.wordpress.com/2015/06/axel.png)

```bash
-v berguna buat verbose atau log2
-n Number of connection , yaitu memecah file yg didownload
-a alternative view ,jd hanya 1 bar yang terlihat ,bisa liat gambar
```

untuk liat opsi atau pertolongan tinggal tulis `man axel`

Oke sekian terima kasih
