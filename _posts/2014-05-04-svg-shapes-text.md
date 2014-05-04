---
layout: post
title: SVG Shapes之文本 &lt;text&gt;
date: 2014-05-04 12:08
author: admin
comments: true
categories: [Svg]
tags: [Svg,shape,text]
---

##8.文本 &lt;text&gt;

####示例8.1
写一个文本：

<svg height="30" width="200">
  <text x="0" y="15" fill="red">欢迎访问wwww.waylau.com </text>
</svg>

	 <svg height="30" width="200">
	  <text x="0" y="15" fill="red">欢迎访问wwww.waylau.com </text>
	</svg>

####示例8.2
让文本转个角度：

<svg height="60" width="200">
  <text x="0" y="15" fill="red" transform="rotate(10 20,40)">欢迎访问wwww.waylau.com</text>
</svg>

	<svg height="60" width="200">
	  <text x="0" y="15" fill="red" transform="rotate(10 20,40)">欢迎访问wwww.waylau.com</text>
	</svg>

####示例8.3
让文本引用path：
 
<svg width="500" height="200">
<defs>
<path id="myTextPath2"
  d="M75,20 l100,0 l100,30 q0,100 150,100"/>
</defs>
<text x="10" y="100" style="stroke: #ff0000;">
<textPath xlink:href="#myTextPath2">
  欢迎访问www.waylau.com个人博客欢迎访问www.waylau.com
</textPath>
</text>
</svg>


	<svg width="500" height="220">
	 <defs>
	   <path id="myTextPath2"
	   d="M75,20 l100,0 l100,30 q0,100 150,100"/>
	</defs>
	
	<text x="10" y="100" style="stroke: #000000;">
	   <textPath xlink:href="#myTextPath2">
	   欢迎访问www.waylau.com个人博客欢迎访问www.waylau.com
	  </textPath>
	</text>  
	</svg>

####示例8.4

可以使用 &lt;tspan&gt; 将文本元素分成几部分，允许每部分有各自的样式

<svg height="90" width="200">
  <text x="10" y="20" style="fill:red;">Several lines:
   <tspan x="10" y="45">欢迎访问</tspan>
   <tspan x="10" y="70">wwww.waylau.com</tspan>
  </text>
</svg>
	
	<svg height="90" width="200">
	  <text x="10" y="20" style="fill:red;">Several lines:
	    <tspan x="10" y="45">欢迎访问</tspan>
	    <tspan x="10" y="70">wwww.waylau.com</tspan>
	  </text>
	</svg>

####示例8.5
使用 &lt;a&gt; 使文本变成一个链接

<svg height="30" width="200" xmlns:xlink="http://www.w3.org/1999/xlink">
  <a xlink:href="http://www.waylau.com" target="_blank">
   <text x="0" y="15" fill="red">欢迎访问wwww.waylau.com
   </text>
  </a>
</svg>

	<svg height="30" width="200" xmlns:xlink="http://www.w3.org/1999/xlink">
	  <a xlink:href="http://www.waylau.com" target="_blank">
	    <text x="0" y="15" fill="red">欢迎访问wwww.waylau.com</text>
	  </a>
	</svg>

####示例8.6
垂直样式

<svg height="260" width="200">
<text x="10" y="10" fill="red" style="writing-mode: tb; glyph-orientation-vertical: 0;">
   欢迎访问wwww.waylau.com
</text>
<text x="110" y="10" fill="red"  style="writing-mode: tb; glyph-orientation-vertical: 90;">
   欢迎访问wwww.waylau.com
</text> 
</svg>

	<svg height="260" width="200">
	<text x="10" y="10" fill="red" style="writing-mode: tb; glyph-orientation-vertical: 0;">
	   欢迎访问wwww.waylau.com
	</text>
	<text x="110" y="10" fill="red"  style="writing-mode: tb; glyph-orientation-vertical: 90;">
	   欢迎访问wwww.waylau.com
	</text> 
	</svg>
