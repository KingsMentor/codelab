Hosting your static site on Google App Engine gives you greater flexibility than using Github Pages and may potentially be cheaper and more configurable than Amazon AWS. Using Google App Engine allows:

* fine grained HTTP cache control for pages and assets,
* HTTP/2 support including server push `Link: "</assets/style.css>; rel=preload; as=style,"`, and
* custom jekyll plugins not permitted by Github Pages, such as `jekyll-assets`
* execute custom server code at your own will 

This basically gives your more than what static pages offers.

### Getting Started

These instructions assume you already have a [Google App Engine Accounnt](https://console.cloud.google.com)

#### 1. Reconfigure Jekyll configuration file `_config.yaml`

1. add `permalink:         /posts/:title` to `_config.yaml`
This tells jekkyll to generate all your post as `postname`.html  in the posts directory. Copy `_site` folder after running `jekyll serve` on paste on the root of your app engine project


**Note!** This is very important as it would affect how your files would be reference when hosted on app engine.
{: .notice}

#### 2. Configure your App Engine Project 

open `app.yaml` and paste:

{% highlight yaml %}

application: app-id
version: 1
runtime: python27
api_version: 1
threadsafe: false


handlers:

- url: /(.*\.(jpg|png|ico))
  mime_type: image/png
  static_files: _site/\1
  upload: _site/(.*\.img)

- url: /(.*\.js)
  mime_type: text/javascript
  static_files: _site/\1
  upload: _site/(.*\.js)

- url: /(.*\.css)
  mime_type: text/css
  static_files: _site/\1
  upload: _site/(.*\.css)

- url: /(.*\.(eot|svg|svgz|otf|ttf|woff|woff2))
  static_files: _site/\1
  upload: _site/(.*\.fonts)

- url: /img
  static_dir: _site/img

- url: /fonts
  static_dir: _site/fonts

- url: /(.*)
  script: main.py

{% endhighlight %}


**Note!** `threadsafe: false`  and the order of arrangment of the app handlers.
{: .notice}

#### 3. Scripting the static pages
Stopping at step 2 wouldn't do much for us. We have to tell app engine on how to route calls.
Hence, we have in `app.yaml` 

{% highlight yaml %}

- url: /(.*)
  script: main.py

{% endhighlight %}

In the main.py, paste this code :

```python
import os

from google.appengine.ext import webapp
from google.appengine.ext.webapp.util import run_wsgi_app

from google.appengine.ext.webapp import template


class Post(webapp.RequestHandler):
    def get(self, *ar, **kw):
        index_path = iteratePath(ar[0])
        try:
            if isPost(index_path):
                path = os.path.join(os.path.dirname(__file__), '_site/' + index_path + '.html')
            else:
                path = os.path.join(os.path.dirname(__file__), '_site/' + index_path + '/index.html')
            self.response.out.write(template.render(path, {}))
        except:
            path = os.path.join(os.path.dirname(__file__), '_site/error.html')
            self.response.out.write(template.render(path, {}))


def iteratePath(path):
    while str(path).endswith("/"):
        path = path[0:(len(path) - 1)]
    return path


def isPost(path):
    return str(path).startswith("posts/")


run_wsgi_app(webapp.WSGIApplication(
        [
            (r'/(.*)', Post),
        ]
        ,
        debug=True))
```

`iteratePath(path)` helps remove any preceding `/` from the url. 
So, if a user is trying to visit `your_site.appspot.com/tags//`, this method helps make sure appegnine make reference to `tags/index.html` by returning `tags` so that  `_site/tags/index.html` can be rendered.

## Handling Custom Error Page

In our main.py, you would notice that a try and catch mechanism was implemented. For this illustration, the catch exception is generic. We basically render `_site/error.html` when there is a problem in loading the page. [See an error page](http://www.belvi.xyz/page_not_found/illustration) To render different custom error page, add the exception name like:

{% highlight python %}
try:
      path = os.path.join(os.path.dirname(__file__), '_site/' + index_path + '/index.html')
      self.response.out.write(template.render(path, {}))
except BaseException, OverflowError:
      path = os.path.join(os.path.dirname(__file__), '_site/error.html')
      self.response.out.write(template.render(path, {}))
{% endhighlight %}

## Wrapping Up

As you can see, you implement your own logic by scripting the static page. This and many more are advantages of hosting jekyll on google app engine. 

I would love to know if this article helped anyone and I honestly want to see wonderful stuff it helped you churn out. <br/>
Thanks.<br/>
*Belvi - I Beliv*
