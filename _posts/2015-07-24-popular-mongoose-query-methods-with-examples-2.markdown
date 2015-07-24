---
layout:     post
title:      "Popular Mongoose Query Methods with Examples 2"
subtitle:   "More on mongoose query methods"
date:       2015-07-24 10:13:00
author:     "Christian Nwamba"
header-img: "img/post-mongoose-queries.jpg"
tags: ["mongoose", "node", "express"]
comments: true
addthis: true
---

<p>In the <a href="{{site.baseUrl}}/2015/07/24/popular-mongoose-query-methods-with-examples">Previous Post</a>
I introduced some query methods in mongoose. We will dive a little bit deeper into this topic with
this post.
</p>

<h3>skip()</h3>
<p>
    Sometimes, you might want to offset an array of data and start at a given row; <code>skip()</code>
    is for you
</p>

<pre class="line-numbers" data-line="1"><code class="language-javascript">
Nerds.find().skip(50).exec(callback);
</code></pre>
<hr>


<h3>limit()</h3>
<p>
    You might not always wnat to fetch dat from beginning to end, <code>limit()</code> would
    assist you to trim an array of data from the bottom
</p>
<pre class="line-numbers" data-line="1"><code class="language-javascript">
    Nerds.find().skip(50).limit(100).exec(callback);
</code></pre>
<hr>

<h3>sort()</h3>
<p>
    Sorting is quite broad in mongoose. I will cover the two main thing you always want 
    to do with <code>sort()</code> and you can't get the rest of the info you need from 
    Mongoose documentation.
</p>
<pre class="line-numbers" data-line="1"><code class="language-javascript">
    Nerds.find().sort('age').exec(callback);
    Nerds.find().sort('-age').exec(callback);
</code></pre>
<p>
    <code>Line 1</code> sorts in ascending order while <code>Line 2</code>
    sorts in a reverse chronological order (descending)
</p>
<hr>

<h3>select()</h3>
<p>
    One other method that causes traffic in Stack Overflow is <code>select()</code>.
    This method simply exculdes or includes fields
</p>
<pre class="line-numbers" data-line="1"><code class="language-javascript">
    Nerds.find().select('name gender age -password -_id').exec(callback);
</code></pre>
<p>
    The above code requests for name, gender and age of nerds but insists that it doesn't
    fetch password and id for security reasons
</p>
<hr>

<h3>equals()</h3>
<p>
    As the name implies, selects field where a a field equals a value
</p>
<pre class="line-numbers"><code class="language-javascript">
    Nerds.where('age').equals(50);
    Nerds.where('name').equals('Chris');
</code></pre>
<hr>

<h3>gte() &amp; lte()</h3>
<p>
    These are just lie <code>gt()</code> and <code>lt()</code> as discussed in the previous post
    but compares for equality too. That is greater than and equal to or less 
    than and equal to.
</p>
<hr>

<h3>count()</h3>
<p>
    Returs the total number of rows in a query
</p>
<pre class="line-numbers"><code class="language-javascript">
    Nerds.find().count().exec(function(err, count){
    
    });
</code></pre>
<hr>

<h3>The almighty $regex()</h3>
<p>
    This is a very popular one an I will show you how to use it
    for the most common task in application of queries: search.
</p>
<pre class="line-numbers"><code class="language-javascript">
    Nerds.find({ "name": { "$regex": "Amanda", "$options": "i" } }, function(err,docs) { 
        
    });
</code></pre>
<p>Sincerely, I do not like to lie, I am not good with regex but that simple code is what I
use for my search queries and it works like <code>CONTAINS</code> in <code>SQL</code>.
Note that you must specify the <code>$option</code> and pass it a value of <code>i</code>
</p>
<hr>

<h2>Conclusion</h2>
<p>We can end now!</p>
<p>These are just commonly used queries that you will meet every day if you
are working with mongoose. Mongoose has lots of other powerful queries which you can explore
if you are unable to find what you are looking for here. Bye!</p>