---
layout:     post
title:      "Popular Mongoose Query Methods with Examples"
subtitle:   "List of most used and important mongoose query methods"
date:       2015-07-24 1:29:00
author:     "Christian Nwamba"
header-img: "img/post-mongoose-queries.jpg"
tags: ["mongoose", "node"]
comments: true
addthis: true
---

<blockquote>Let's face it, writing MongoDB validation, casting and business logic boilerplate is a drag. That's why we wrote Mongoose. - <a href="mongoosejs.com">Mongoose</a></blockquote>

<h2 class="section-heading">Overview?</h2>

<p>
<a href="mongoosejs.com">Mongoose</a> basically is a node library which simplifies the use of Mongo DB
in node application. It also provides a means to model data just as you could in every other MVC framework. 
It is simple and straight foward.
</p>

<p>This article will not introduce you formally to Mongoose or Mongo but assumes that you have a basic
knowledge of what these technologies are and will help you with important use of Mongoose methods.</p>

<p>
    I am also assuming that you know how to create a <code>Schema</code> and <code>Model</code> 
    and that we have a Model called <code>Nerds</code> and stored in a variable
    <code>Nerds</code>. I will also be using these methods in a Node context for better understanding.
</p>

<p>Ok, Enough! I really have phoebia for a lot of English unless if necessary, lets code...</p>


<h3>find()</h3>
<p>
    The <code>find()</code> method when used on <code>Nerds</code> will return all Nerds in the database.
</p>
<pre class="line-numbers" data-line="2-5"><code class="language-javascript">
    app.get('/nerds', function (req, res) {
        Nerds.find().exec(function (err, nerds) {
            console.log(nerds);
            res.json(nerds);
        });
    });
</code></pre>
<p>
    As you can see, line 2 to 5 are highlighted as that is actually where Mongoose magic happens.
    The exec() is just as good as a callback function and can be used so. It takes care of what ever
    happens after the find() method is executed
</p>

<p>
    find() is the most used query in mongoose and can come in flavors like:
</p>
<pre class="line-numbers" data-line="2"><code class="language-javascript">
    app.get('/nerds', function (req, res) {
        Nerds.find({gender:female}).exec(function (err, nerds) {
            console.log(nerds);
            res.json(nerds);
        });
    });
</code></pre>
<span class="caption text-muted">Get all Nerds that are female</span>
<hr>
<h3>findOne()</h3>
<p>
    The <code>findOne()</code> method will return one nerd while matching a given criteria and if there
    are multiple data that matched the criteria, the first will be returned.
</p>
<pre class="line-numbers" data-line="2-5"><code class="language-javascript">
    app.get('/nerds', function (req, res) {
        Nerds.findOne({firstName:'Bill'}).exec(function (err, nerd) {
            console.log(nerd);
            res.json(nerd);
        });
    });
</code></pre>
<hr>

<h3>findById()</h3>
<p>
    If you have played with Mongo before, you will observe that it attaches a unique ID to it's
    record. With <code>findById()</code> you can get a particular record using it's Id as the name implies
</p>
<pre class="line-numbers" data-line="2-5"><code class="language-javascript">
    app.get('/nerds', function (req, res) {
        Nerds.findById('5224bb2j3232h422312').exec(function (err, nerd) {
            console.log(nerd);
            res.json(nerd);
        });
    });
</code></pre>
<hr>

<h3>where()</h3>
<p>
    <code>where()</code> is a multi-purpose mongoose method that has the capability of performing find queries and much more> below are some of the examples    
</p>

<pre class="line-numbers" data-line="1"><code class="language-javascript">
Nerds.where('age').gte(18).lte(20).exec(callback);
</code></pre>

<p>It can also be chained:</p>

<pre class="line-numbers" data-line="1"><code class="language-javascript">
Nerds
 .where('age').gte(18).lte(20)
 .where('gender', 'Male').exec(callback);
</code></pre>
<hr>

<h3>gt() &amp; lt()</h3>
<p>
    <code>gt()</code> stands for greater than and takes a number as argument. 
    <code>lt()</code> as well is less than and also takes a number argument.
    Yes, it is what you are thinking right now. Check if greater than or less than
    the passed arguent.
</p>

<pre class="line-numbers" data-line="1"><code class="language-javascript">
Nerds.where('age').gte(18).exec(callback);
</code></pre>

<pre class="line-numbers" data-line="1"><code class="language-javascript">
Nerds.where('age').lte(20).exec(callback);
</code></pre>

<h2>Conclusion</h2>
<p>Not so fast!</p>
<p>Let's get a cup a coffee and continue in the next section</p>
<p><a href="">Popular Mongoose Query Methods with Examples 2</a></p>