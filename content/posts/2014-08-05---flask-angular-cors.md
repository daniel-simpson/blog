---
title: Flask, AngularJS and CORS
date: "2014-08-05"
template: "post"
draft: false
slug: "/posts/2014/flask-angular-cors/"

tags:
- "web"
- "angularjs"
- "python"
- "flask"
- "programming"
- "development"
description: "I am currently developing a website that will entirely be a Single Page Application (SPA).  I started building the back-end in D and the front-end in AngularJS.  I decided after a couple of weeks that Jeff Atwood was right in saying 'Storage is cheap, programmers are expensive.'  Though D is a useful language, it was taking me too long to produce useful RESTful API endpoints, so I decided to make the switch to Flask given my familiarity with it."
---
I am currently developing a website that will entirely be a Single Page Application (SPA).  I started building the back-end in D and the front-end in AngularJS.  I decided after a couple of weeks that [Jeff Atwood](http://www.codinghorror.com) was right in saying "Storage is cheap, programmers are expensive."  Though D is a useful language, it was taking me too long to produce useful RESTful API endpoints, so I decided to make the switch to [Flask](http://flask.pocoo.com) given my familiarity with it.

In the first iteration of the project I had a simple index.html being served from the same application that the API was running, accessing all my scripts, styles, images, etc... from a CDN.  This was a fairly simple CORS setup and a little bit of tweaking in Angular to make it all work.

When I made the switch to Flask I changed the structure of the hosting so that the static content was being served from `www.example.com` and the API was accessed from `api.example.com`.  I figured this wouldn't cause too many issues and it should again just be a simple CORS setup.  Unfortunately there was a little more to it than that.  I found that when making requests with Angular's `$http` provider cookies that were being set were immediately being discareded.  I ended up routing all my requests through nginx so that the API was hosted at `www.example.com/api` and the cookies were being retained correctly.

The solution was simple in the end.  All I needed to do was add the following code to my Angular module `.config()` method.

```js
$httpProvider.defaults.withCredentials = true;
```

On the server-side initially I was using Flask-CORS but it was frustrating to have to decorate all my REST endpoints (essentially every single route in my application) with `@cross_domain()`, so I ended up writing my own basic Flask context processor.

```python
@app.after_request
def add_cors_headers(response):
    response.headers.add('Access-Control-Allow-Origin', 'www.example.com')
    response.headers.add('Access-Control-Allow-Credentials', 'true')
    response.headers.add('Access-Control-Allow-Headers', 'Content-Type')
    return response
```

The `Access-Control-Allow-Credentials` is necessary when specifying `withCredentials` on `$http` requests.