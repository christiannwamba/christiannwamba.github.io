---
layout:     post
title:      "Animation using ngAnimate and Animate.css"
subtitle:   "Animation have never been so fast an easy"
date:       2015-07-28 12:49:00
author:     "Christian Nwamba"
header-img: "img/posts/ng-animate-css.jpg"
tags: ["angular"]
comments: true
addthis: true
---

<h3>Overview</h3>
<p>
    <a href="http://angularjs.org">Angular</a> has had series of evolution. Animation in angular
    did not find it funny with this evolving process until now. Before Angular 1.2, we
    could not not easily apply CC3 animation because it was JS hard-coded. Angular 1.2 made it
    dead easy to use our awesome CSS3 animations with angular just by including a new dependency
</p>

<p>
    <a href="https://daneden.github.io/animate.css/">Animate.css</a> is a library
    that serves a lot of CSS3 animation sample that would do for any thing you would want to
    do with animation on the Web.
</p>

<h3>How</h3>
<p>
    It is simple as I already said, just:
</p>
<ol>
    <li>Setup your angular application</li>
    <li>Add <code>angular-animate</code> script to your project</li>
    <li>Add ngAnimate as dependency</li>
    <pre>
        <code  class="language-javascript">
            var app = angular.module('app', ['ngAnimate']);
        </code>
    </pre>
    <li>ngAnimate adds one or more of three classes to a DOM to be animated: <code>ng-enter</code>, 
    <code>ng-leave</code> and <code>ng-move</code>. The names implies exactly how they work. Adding animation styles
    to any of this class does the magic.
    </li>
    <li>Include the Animate.css library and use the styles as shown in the codepen sample</li>
</ol>

<h3>Example</h3>
<p>I made a sample simple Todo application on codepen.
It illustrates what I have been blabing since:
</p>
<div data-height="268" data-theme-id="12518" data-slug-hash="bdQGzx" data-default-tab="html" data-user="christiannwamba" class='codepen'><pre><code>&lt;div ng-app=&quot;app&quot; ng-controller=&quot;TodoCtrl&quot; class=&quot;container&quot; style=&quot;margin-top:50px&quot;&gt;
  &lt;div class=&quot;form-group&quot;&gt;
    &lt;label&gt;Todo&lt;/label&gt;
    &lt;input type=&quot;text&quot; class=&quot;form-control&quot; ng-model=&quot;title&quot; placeholder=&quot;Enter a  todo&quot; /&gt;
    &lt;button class=&quot;btn btn-primary&quot; ng-click=&quot;add()&quot;&gt;Add&lt;/button&gt;
  &lt;/div&gt;
  &lt;table class=&quot;table&quot;&gt;
    &lt;tr&gt;
      &lt;td&gt;Todo&lt;/td&gt;
      &lt;td&gt;Delete&lt;/td&gt;
    &lt;/tr&gt;
    &lt;tr ng-repeat=&quot;t in todos&quot; class=&quot;todo&quot;&gt;
      &lt;td&gt;{{t.title}}&lt;/td&gt;
      &lt;td&gt;&lt;a class=&quot;btn btn-danger&quot; ng-click=&quot;remove($index)&quot;&gt;Delete&lt;/a&gt;&lt;/td&gt;
    &lt;/tr&gt;
  &lt;/table&gt;
&lt;/div&gt;</code></pre>
<p>See the Pen <a href='http://codepen.io/christiannwamba/pen/bdQGzx/'>Animate Css</a> by Chris Nwamba (<a href='http://codepen.io/christiannwamba'>@christiannwamba</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
</div><script async src="//assets.codepen.io/assets/embed/ei.js"></script>

<p>
    Add and deleting todo creates a simple animation effects
</p>

<h3>Things to Note</h3>
<ul>
    <li>The ngAnimate dependency.</li>
    <li>The animate property's value: <code>fadeInLeft 1s</code> and <code>bounceOut 1s</code>
    are contained in Animate.css and varities can be found at the Git Hub Repo.</li>
    <li><code>ng-enter</code> and <code>ng-leave</code> are attached to the elements
    we want to create effects for.</li>
</ul>

<h3>Finally!!!</h3>
<p>
    You have seen how dead simple that was. Go ahead and wow the world with it...... Thanks!
</p>