# Integrating Google Analytics in Django
Google analytics is an integral part of almost any website. Integration requires pasting a simple JavaScript in your webpage.

Things to take in mind:

- Making it more configurable, without overkilling with a standalone django app.
- Actually disabling google analytics for everything that's not production - we don't want to track fake views.

> Read more [here](https://www.hacksoft.io/blog/integrating-a-production-only-google-analytics-in-django)

## Using custom context processor

- Here's a snippet from my `context_processor` file:

```py
from django.conf import settings
from django.template.loader import render_to_string

def analytics(request):
    """
    Returns analytics code.
    """
    if not settings.DEBUG:
        return { 'analytics_code': render_to_string("analytics/analytics.html", { 'google_analytics_key: settings.GOOGLE_ANALYTICS_KEY }) }
    else:
        return { 'analytics_code': "" }
```

- Of course you'll need to tell Django to include this in your context. In in your `settings.py` file, include:

```py
TEMPLATE_CONTEXT_PROCESSORS = (
    ...
    "context_processors.analytics",
)
```

> I have it set up to include the analytics code only when `DEBUG` is set to False, but you may prefer to key it off something else, perhaps a new setting altogether. I think DEBUG is a good default since it supposes you don't want to track any hits while debugging/developing.

- Create a setting with your Google Analytics Key:

```py
GOOGLE_ANALYTICS_KEY = "UA-1234567-8"
```

- Create a template called: `analytics/analytics.html` that includes something like this:

```html
<script type="text/javascript">
var gaJsHost = (("https:" == document.location.protocol) ? "https://ssl." : "http://www.");
document.write(unescape("%3Cscript src='" + gaJsHost + "google-analytics.com/ga.js' type='text/javascript'%3E%3C/script%3E"));
</script>
<script type="text/javascript">
try {
var pageTracker = _gat._getTracker("{{ google_analytics_key }}");
pageTracker._trackPageview();
} catch(err) {}</script>
```

- Finally, just before the closing tag in your `base.html` template, add this:

```html
{{ analytics_code }}
```

- Now your analytics code will be included only when `DEBUG=False`. Otherwise, nothing will be included.

## Using Package
There's a reusable Django app called [**django-google-analytics**](http://github.com/montylounge/django-google-analytics). The easiest way to use it is:

- Add the `google_analytics` application to your `INSTALLED_APPS` section of your `settings.py`.
- In your base template, usually a `base.html`, insert this tag at the very top: `{% load analytics %}`
- In the same template, insert the following code right before the closing body tag: `{% analytics "UA-xxxxxx-x" %}` the `UA-xxxxxx-x` is a unique Google Analytics code for your domain.

---
