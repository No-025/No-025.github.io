---
title: "210316-나를 소개하는 홈페이지 만들기"
categories:
  - Spring
  - CSS
---

CSS

```CSS
@charset "UTF-8";

body {
	margin: auto;
	padding: 10px;
	background-color: gray;
	overflow: scroll;
}

a {
	text-decoration: none;
}

h1{
	font-size: xx-large;
}

h2{
	font-size: x-large;
	margin-top: 0;
	margin-bottom: 0;
}


nav{
	padding: 10px;
	background-color: white;
	overflow: hidden;
}

p{
	padding-top: 10px;
}

hr{
	clear: both;
	width: 98%;
}

.nav_ul{
	list-style-type: none;
	float: right;
}

.nav_li{
	width: 140px;
	line-height: 40px;
	background-color: #87CEEB;
	box-shadow: 2px 2px 2px 2px gray;
	margin:7px;
	text-align: center;
	float: left;
}

.nav_a{
	color: purple;
}

.index_section{
	text-align: center;
	background: white;
	margin-top: 20px;
	margin-bottom: 20px;
	padding: 50px;
}

.index_ul{
	text-align: center;
	padding: 0;
}

.index_li{
	display: inline-block;
	width: 140px;
	line-height: 130px;
	background-color: #87CEEB;
	box-shadow: 2px 2px 2px 2px gray;
	margin:5px;
}

.index_a{
	color: white;
}

.aboutme_section{
	background: white;
	margin-top: 20px;
	margin-bottom: 20px;
	padding-left: 120px;
	padding-right: 120px;
}

.photo_section{
	background: white;
	margin-top: 20px;
	margin-bottom: 20px;
	overflow: hidden;
}

.photo_img{
	border: 10px solid gray;
	width: 400px;
	margin: 50px;
	float: left;
}

.photo_p{
	line-height: 2;
	margin: 50px;
	
}

.footer_center{
	text-align: center;
	background: white;
	cursor: pointer;
	padding: 20px;
	color: gray;
}
```
