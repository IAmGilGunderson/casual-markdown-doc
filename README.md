## Casual-Markdown-Doc

[Casual-Markdown-Doc](https://github.com/casualwriter/casual-markdown-doc) provide a quick solution 
to use markdown as document.

* include javascript lib `casual-markdown-doc.js`
* include css style `casual-markdown-doc.css`

then start write document in markdown format!

check the sample document
at https://casualwriter.github.io/casual-markdown/casual-markdown-syntax.html


### Usage Guide

1. create your document in html format. e.g. `casual-markdown-syntax.html` 
2. use below first 4 line as header, and start draft content in markdown format
3. at line 4, revise title to your document title
4. start draft document in markdown format

~~~
<!DOCTYPE html>
<link  href="https://casualwriter.github.io/dist/casual-markdown-doc.css" rel="stylesheet">
<script src="https://casualwriter.github.io/dist/casual-markdown-doc.js"></script>
<body title="Supported Syntax of Casual-Markdown">
## Heading
content in markdown format
~~~

or include `casual-markdown-doc.js` from local

~~~
<!DOCTYPE html>
<link  href="casual-markdown-doc.css" rel="stylesheet">
<script src="casual-markdown-doc.js"></script>
<body title="Supported Syntax of Casual-Markdown">
## Heading
content in markdown format
~~~

### Table of Content 

* table-of-content will be auto-generated from markdown heading
* hotkey [alt-t] to toggle table-of-content popup-box
* hotkey [ctrl-p] to print document, table-of-content will be inserted as first page automatically.
* if donot want table-of-content printout. please close TOC box first, then print document.

### How it works

The main program is very simple by doing the following steps. (in 15 lines).

1. read markdown content from ``<body>``
1. update document title 
2. call casual-markdown parse, convert to html and update to content area.
3. generate table-of-content with scrollspy feature.

~~~
//=============================================================================
// 20220719, convert markdown-document in <body> tag into HTML document
//=============================================================================
window.onload = function () {

  var html = '<div class="container" style="margin:auto; max-width:1024px; padding:4px;">'
  html += '<header id=heading>' + (document.body.title||document.title) + '</header>'
  html += '\n<div id=tocbox><button style="float:right" onclick="this.parentElement.style.display=\'none\'">'
  html += 'X</button><div id="toc"></div></div>' 
  html += '\n<div id=content>' + md.html(document.body.innerHTML.replace(/\&gt;/g,'>')) + '</div></div>'; 

  // add shortcut for edit current page.
  html += '<a href=# onclick="tocToggle()" accesskey=t style="display:none">TOC</a>';
  html += '<a href=# onclick="debug()" accesskey=x style="display:none">HTML</a>';
  
  document.body.innerHTML = html
  document.body.style.display = 'block';
  md.toc( 'content', 'toc', { scrollspy:'body' } )
  
}
~~~


### Modification History

* 2022/07/22, v0.70, initial release.
 
