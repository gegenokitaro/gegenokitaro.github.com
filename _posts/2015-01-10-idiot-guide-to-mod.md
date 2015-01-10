---
layout: post
title: "Idiot guide to Desktop Modding (Bahasa)"
description: ""
category: 
tags: []
---
{% include JB/setup %}

### #1 Complete Newbie

Saya sering wondering, gimana ya cara bikin desktop kayak gini, cara bikin desktop kayak gitu. Sedangkan saya sendiri <i>nda</i> tau apa-apa. Ini pertama kali nya saya modding desktop, bahkan pertama kali nya saya <i>nginstall</i> distro basis linux. Saya pernah lihat <i>screenshot</i> dari desktop linux, bagus-bagus, dan saya pingin desktop saya juga jadi bagus. Terus saya <i>kudu ngapain</i>?

Saya <i>nanya</i> aja ah ke forum-forum, "Bagaimana cara bikin desktop saya jadi bagus". Yey, cara cepet banget biar dapet ilmu instan. Tapi kok jawabannya malah bikin bingung ya.. 

"Install DE ini blablabla..." 

"Ganti ini blablabla" 

"Kasih conky blablabla..." 

"Blablabla..." 

"Kayaknya situ masi belum paham yang situ tanyakan blablabla..."

Apa maksudnya ini semua? Saya jadi makin bingung... Apa itu DE, apa itu conky, ntar saya malah nanya apa itu DE, apa itu conky, installnya bagaimana, dll.. pilihan yang buruk. Terus gimana cara nya biar bisa modding desktop.. saya kepengen banget. Saya bener-bener butuh bantuan.

Akhirnya, saya memutuskan untuk bertapa sejenak. Saya kudu cari-cari sendiri apa maksud dari semua ini. Oke, baiklah, pertama-tama, saya kudu belajar bahasa Inggris. Kebetulan saya pake Ubuntu, dan desktop nya ya gitu-gitu aja. Apa nama desktop ini? Google dulu ah..

<br>
<img src="/img/ubuntudefaultdesktop.png" style="border: 2px solid #6f6f6f">

Oh namanya Unity ternyata. Bentar-bentar.. apa itu unity? Kudu googling dulu, paling enggak mampir ke wikipedia.

<br>
<img src="/img/unityuserinterface.png" style="border: 2px solid #6f6f6f">

<br>
Ih.. tambah bingung.. gimana ini.. Santai, jangan panik dulu. Kata google, Unity itu default desktop environment nya Ubuntu. Desktop Environment. Desktop Environment, kok kayaknya familiar ya.. bentar, kalo disingkat, berarti jadi.. DE! Ya, DE!! ada komen di pertanyaan saya yang jawabannya ganti DE. Apakah DE itu maksudnya adalah seperti yang saya maksud? Coba cari dulu ah di google.

Setelah saya cari-cari, ternyata memang DE itu adalah lingkungan desktop yang saat ini saya jalankan. Oh jadi begitu.. Terus, saya kudu ngapain ya.. Ganti tema? Dikasih apa gitu? Oke, akan saya cari di google!

------------------------------------------------------------------------------------------------

Cuplikan cerita diatas itu mungkin pernah kita alami, dengan berbagai macam variasi simpulan dan petualangan. Dengan adanya forum, grup, komunitas, dll memang kita dimudahkan untuk saling berbagi ilmu dan bertanya. Namun, jangan lah sampai kita jadi `vampire` dalam suatu komunitas, dengan menanyakan hal-hal sepele yang seharusnya dapat digali informasinya secara mandiri.

`Idiot Guide to Mod` merupakan salah satu cara saya untuk mengkritik fenomena yang sering terjadi dalam sebuah komunitas. Dengan adanya kritik ini, saya juga memiliki tanggung jawab atas sebuah solusi atas kritik saya. Karena itu, berikut ini solusi-solusi yang saya tawarkan atas permasalahan diatas. Solusi saya ini lebih banyak bersifat teknis, karena itu, silahkan dikritik kembali.

Apa itu desktop modding?

Menurut saya sendiri,desktop modding adalah suatu usaha untuk memperindah suatu tampilan yang kita gunakan. Modding sendiri memerlukan beberapa skill teknis untuk dapat menghasilkan suatu karya yang dapat diterima dengan baik.

Untuk para pendatang baru, harus mulai darimana?

<b>1. Kenali mesin yang anda pakai.</b>

Mulai dari DE (Desktop Environment), aplikasi yang dipakai, cara <i>theming</i>, dll. Bagaimana kita bisa memodifikasi Desktop Environment yang kita pakai kalau kita sendiri belum tahu apa itu Desktop Environment.

<b>DE</b> menurut saya merupakan suatu kumpulan dari berbagai macam aplikasi yang saling membangun untuk menciptakan suatu lingkungan desktop yang layak dihuni. Tapi, apakah pengertian seperti ini yang dibutuhkan dalam desktop modding? Sedikit ya, dan kebanyakan tidak. Untuk pertama kalinya desktop modding, pengetahuan tentang DE yang dibutuhkan adalah pengetahuan tentang macam-macam DE. Apa saja macam-macam DE dan bagaimana tampilannya. Itu. Itu yang perlu diketahui. Jadi kita bisa membandingkan mana DE yang paling bagus dan mulai mendalami nya. 

Mau coba-coba, silahkan, itu malah lebih bagus. Dengan seringnya coba-coba, kita akan lebih sering juga menghadapi permasalahan. Dari permasalahan lah ilmu itu datang.

Misal seperti ini.

![leublu](/img/leublu.png)

	Gnome-Shell, GTK theme by me forked from Kyun
	plank theme by me forked from Kyun
	icon set ~ Numix
	running apps ~ Rhythmbox, Gcolor3, Urxvt

Bisa kita lihat disana menggunakan `Gnome-shell`, `plank` sebagai dock, dan aplikasi-aplikasi yang ditunjukkan adalah `Rhythmbox`, `Gcolor3` dan `Rxvt-Unicode`. Tau darimana? dari keterangannya kan? Dari situ kita bisa mempelajari bagian-bagian dari sebuah desktop. Dari keterangan tersebut kita bisa mulai mencari dan mempelajari desktop modding. Karena itu, jika anda memiliki kelebihan dalam hal desktop modding, jangan lupa cantumkan sedetail mungkin keterangan tentang desktop anda. Itu sangat berguna bagi kami para newbie.

<b>2. Do it yourself.</b>

Saya sering <i>jalan-jalan</i> ke DeviantArt dan menemukan karya seni yang epic, misal, sebuah konfigurasi `conky` yang sangat memukau untuk dipasang di desktop. Apa itu conky? Saya sendiri masih belum tahu apa itu conky, sedangkan pada <i>screenshot</i> yang ditunjukkan di DeviantArt, jelas-jelas itu sangat indah. Dari kata kunci ini: `conky`, kita bisa mulai mencari apa dan bagaimana sebuah conky itu. Apa conky itu dan bagaimana cara memasangnya. Oke, setelah mencari beberapa saat, saya menemukan cara untuk memasang conky. Dengan `conky -c /path/to/conky/config` saya dapat memunculkan conky di desktop saya. Semudah itu? Ya, semudah itu. Dengan adanya `conky manager`, hal tersebut malah membuat semua makin mudah. Sekali lagi, dengan adanya kata kunci `conky manager`, kita dapat mencari dan memahami apa itu conky manager. Mungkin, dalam praktis nya, kita akan menemui berbagai permasalahan. Jangan panik. Dengan berbekal kata kunci yang ada, kemungkinan besar permasalahan tersebut akan terpecahkan apabila kita mau berusaha.

Contoh kasus diatas merupakan salah satu dari sekian banyak kasus yang sering kita hadapi dalam desktop modding. Pintar-pintarlah mencari kata kunci. 

<br>
<br>
<br>
masih bersambung
