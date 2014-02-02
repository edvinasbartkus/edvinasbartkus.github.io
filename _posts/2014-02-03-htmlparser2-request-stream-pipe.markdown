---
layout: post
title: "Node: htmlparser2 & request"
date: 2014-02-03 00:40:00
categories: node
---
[htmlparser2](https://github.com/fb55/htmlparser2) - it's the fastest tool for [Node](http://nodejs.org/) to parse HTML/XML. When you need to get a file from the internet you can use [request](https://github.com/mikeal/request) or even more minimal [minreq](https://github.com/mikeal/request) module. Both of them play nicelice with streams. Simply pipe it ;-)

{% gist 8776042 parser.js %}
