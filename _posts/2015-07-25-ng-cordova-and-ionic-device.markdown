---
layout:     post
title:      "ngCordova and Ionic: Device"
subtitle:   "Introduction to ngCordova device plugin using Ionic"
date:       2015-07-25 2:59:00
author:     "Christian Nwamba"
header-img: "img/ionic-ngcordova.jpg"
tags: ["node", "ionic", "android", "cordova", "ng-cordova"]
comments: true
addthis: true
---

<h3>Overview</h3>
<p>
    <a href="http://ionicframework.com">Ionic</a> is a very powerful and popular framework for
    hybrid mobile applicaiton developers. It doesn't take out the work of Cordova or Phonegap but 
    is simply a HTML, CSS and Javascrip framework for the frontend of your application.
</p>

<p>
    <a href="http://ngcordova.com">ngCordova</a> is simply an angular wrapper for Apache Cordova plugins
    and makes it easy to integrate the plugins in ionic because ionic itself is angular driven.
</p>

<p>
    This post is the beginning of a series that will serve as a guide to using Cordova plugins with the
    help of ngCordova. In order to get along with the series, please use an hour to understand
    the basics of ionic.
</p>

<h3 id="setup">Setup</h3>
<p>
    Througout the series, we will be repeating this section. Basically, the setup includes, 
    installing ionic, cordova, setting up an ionic - cordova project 
    and including ngCordova to our ionic project
</p>

<h4>Installation</h4>
To get started, if you have not done this yet, run:
<p>
    <code>npm install -g cordova ionic bower</code>
</p>
<p>
    This will install cordova, ionic and bower for us. If you ain't familiar with
    bower, it is a dependency manager for our static files - HTML, CSS, JS, etc.
    The -g flag is just making it a global dependency so we will not have to install
    in future again unless there are reason for updates.
</p>

<h4>Start</h4>
<p>
    Our next task is to start a new blank ionic project, add cordova and at least one mobile
    platform to it, which will be android.
</p>
<p>
    As this is a series, I will advice you create a folder to house each of the projects.
    cd to the created folder and run:
</p>
<p>
    <code>ionic start device blank</code>
</p>
<p>
    That will generate an ionic project for us with a blank template. There are other
    ionic templates we can use and I will gradually introduce them in the series.
</p>
<p>
    <code>cd device</code>
</p>
<p>
    <code>ionic platform add android</code>
</p>
<p>
    <code>ionic serve --lab</code>
</p>

<p>
    We 'cd' to the folder, add android platform and ran the project.
    It will automatically pop up in the browser
</p>

<h4>Testing</h4>
<p>
    To test our app in a real device, I always use two options
    <ol>
        <li>Use <code>ionic run</code> if a device is connected to port the app to it</li>
        <li>Use <a href="app.phonegap.com">Phonegap App</a> and make sure my PC
        and the phone are on the same network</li>
    </ol>
</p>

<img src="{{site.baseUrl}}/img/screenshots/Screenshot_2015-07-25-20-21-15.png" style="height:400px; width:auto">
<span class="caption text-muted">Default look of app after first run</span>

<h3>Rest of the code</h3>
<h4>Install Device Plugin</h4>
<p>
    The first thing to do after your project is set up is to install the required plugin,
    in this case: device
</p>
<p>
    <code>cordova plugin add org.apache.cordova.device</code>
</p>

<h4>Install ngCordova</h4>
<p>
    <code>bower install ngCordova --save</code>
</p>
<pre>
    <code class="language-markup">
        &lt;!--Make sure it is after ionic and before cordova-->
         &lt;script src="lib/ngCordova/dist/ng-cordova.min.js">&lt;/script>
    </code>
</pre>
<p>Then include as a dependecy to you angular app in <code>www/js/app.js</code></p>
<pre>
    <code class="language-javascript">
        angular.module('starter', ['ionic', 'ngCordova'])
    </code>
</pre>

<p>Update your app.js to look like the following</p>

<pre class="line-numbers" data-line="7-8, 21-27"><code class="language-javascript">
// Ionic Starter App

angular.module('starter', ['ionic', 'ngCordova'])

.run(function($ionicPlatform, $cordovaDevice, $rootScope) {
    $ionicPlatform.ready(function() {
      $rootScope.$emit('cordovaDevice', $cordovaDevice.getDevice());
      $rootScope.$broadcast('cordovaDevice', $cordovaDevice.getDevice());
      //$rootScope.device = $cordovaDevice.getDevice();
      // Hide the accessory bar by default (remove this to show the accessory bar above the keyboard
      // for form inputs)
      if (window.cordova && window.cordova.plugins.Keyboard) {
        cordova.plugins.Keyboard.hideKeyboardAccessoryBar(true);
      }
      if (window.StatusBar) {
        StatusBar.styleDefault();
      }
    });
  })
  .controller('DeviceCtrl', function($ionicPlatform, $scope) {
    console.log($scope.device)
    $scope.$on('cordovaDevice', function(e, d) {
      $scope.device = d;
      console.log(d);
    });
  })
  </code></pre>
  
  <p>
      The only change is on the highlighted lines.
      Line 7-8 uses the <code>$cordovaDevice</code> to broadcast and emit
      an event on the rootscope so that other controllers' scope can use
  </p>
  
  <p>
      Line 21 to 27 is just a controller using <code>cordovaDevice</code>
      event and binding its data to a scope
  </p>
  
  <pre class="line-numbers"><code class="language-markup">
  
  &lt;body ng-app="starter" ng-controller="DeviceCtrl">

  &lt;ion-pane>
    &lt;ion-header-bar class="bar-assertive">
      &lt;h1 class="title">Device Plugin</h1>
    &lt;/ion-header-bar>
    &lt;ion-content>
      &lt;div class="card">
        &lt;ul class="list">
          &lt;li class="item">
            Platorm : &#123;{device.platform}}
          &lt;/li>
          &lt;li class="item">
            Model : &#123;{device.model}}
          &lt;/li>
          &lt;li class="item">
            UUID : &#123;{device.uuid}}
          &lt;/li>
        &lt;/ul>
      &lt;/div>
    &lt;/ion-content>
  &lt;/ion-pane>
&lt;/body>
  
  </code></pre>
  
  <p>
      We attached the controller to the body tag so we can have access to the device
      property of it's scope. The rest is basic HTML and angular. Thats all!
  </p>
  
  <img src="{{site.baseUrl}}/img/screenshots/Screenshot_2015-07-25-22-12-08.png" style="height:600px; width:auto">
  <span class="caption text-muted">Finally!...</span>
  
  <h3>Conclusion</h3>
  <p>
      Remember what I told you in the beginning? This is the beginning if a series on ngCordova.
      To see more on this, click the tags tagged on this article. Thank you for reading.
      I appreciate!...
  </p>