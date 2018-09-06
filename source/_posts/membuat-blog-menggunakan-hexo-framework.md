---
title: membuat blog menggunakan hexo framework
date: 2018-09-05 17:56:41
tags: [web]
categories: [NodeJS]
---

Hexo adalah salah satu blog framework yang handal. Hexo sangatlah simpel dan powerful. Dengan Hexo, anda cukup menulis postingan menggunakan Markdown. Markdown adalah sebuah tool yang mengubah text-to-HTML. Dokumentasi Hexo lebih lengkap [Hexo](https://hexo.io/).

### Tools
Untuk menggunakan Hexo dalam membuat blog, anda perlu menginstal [NodeJS](http://nodejs.org/) dan [GIT](http://git-scm.com/)
<!-- more -->

### Generate blog
Buatkan direktori (folder) untuk menyimpan file-file hasil generate Hexo. Ikuti langkah dibawah: 
``` bash
C:\xampp\htdocs>md hexobase
C:\xampp\htdocs>cd hexobase
C:\xampp\htdocs\hexobase>npm install -g myblog
C:\xampp\htdocs\hexobase>hexo init
C:\xampp\htdocs\hexobase>hexo generate
C:\xampp\htdocs\hexobase>hexo server
```
### Create a new post
Pastinya setelah blog telah terbentuk, anda perlu membuat postingan pada blog. Caranya sangat mudah:
``` bash
$ hexo new "My New Post"
```