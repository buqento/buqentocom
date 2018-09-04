---
title: Simple Webpage
date: 2010-09-19 16:53:39
tags: [PHP]
categories: [PHP]
---

## Quick Start

{% codeblock index.php lang:objc %}
$page = $_GET[page];
if(empty($page)){
    $page="home.php";
}else{
    $page=$_GET[page];
}
include("$page");
{% endcodeblock %}