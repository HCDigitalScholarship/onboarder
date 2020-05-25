---
title: '11 mini-blini project (May 26 PM)'
description:
  "We will add new functionality to a small existing project called blini"
prev: /chapter10
next: /chapter12
type: chapter
id: 11
---

<exercise id="1" title="Minimal Computing">

Alex Gil, ["The User, the Learner and the Machines We Make"](http://go-dh.github.io/mincomp/thoughts/2015/05/21/user-vs-learner/)

Roopika Risam, [New Digital Worlds : Postcolonial Digital Humanities in Theory, Praxis, and Pedagogy](https://tripod.haverford.edu/permalink/01TRI_INST/14s7maf/alma991018902072104921)  

> Minimal computing is an approach to digital humanities design and method that eschews high-performance computing in favor of practices that are more accessible around the world. While digital humanities tools and methods readily available in the Global North tend to keep pace with developments in desktop computing and thus privilege newness, minimal computing takes a different approach to “innovation” in digital humanities, focusing on developing accessible digital humanities projects and practices for low-income economies and low-bandwidth environments. (Risam, p. 43)

- minimal by design 
- more accessible (works even without internet access)
- more secure (no active server)
- less dependent on commercial infrastructure
- reduce environmental impact 
- preservation 

</exercise>


<exercise id="2" title="Blini">

Blini is a minimal site builder built with FastAPI. Users can create digital essays and exhibits that are saved directly to flat HTML files.  Like Google Docs, content is automatically saved. The editing interface is designed to be identical to output HTML. Sites can be exported as a zip file, which can be served on Netlify, S3 or Github pages.

- [repo](https://github.com/apjanco/blini)
- [demo](https://blini.apjan.co/)

</exercise>

<exercise id="3" title="new feature">

Blini uses a text editor called [ckeditor](https://ckeditor.com/).  It gives us all of the formatting and word processing tools that we need.  It formats the text in HTMl, so it's perfect for our purposes.  However, in ckeditor5, there is no longer the option of editing the HTML directly in the editor.  Mike would like this functionality.  

We need:
- the ability to load the raw HTML of a page
- the ability to make edits to the page
- save the edits back to the file 

</exercise>

<exercise id="4" title="the introspective app">

To get us started, I created a simple FastAPI app.
It uses a JS library called [code mirror](https://codemirror.net/).  You've probably seen it on [codepen](https://codepen.io/) and other code sharing sites. 

The code is here:
https://github.com/apjanco/introspective

<img src="introspective.png">
</exercise>