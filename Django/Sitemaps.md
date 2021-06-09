# Sitemaps

A vital part of modern **SEO (Search Engine Optimization)** is to have a sitemap, an XML file that tells a search engine how often a page is updated and how important it is in relation to other pages on the site.

- Django comes with a built-in sitemap framework to help in this task.
- Generally, a sitemap exists at a single location as a `sitemap.xml`.

## Installation
- To add a sitemap, we must install the `sitemap` app to our project as well as the `sites` framework which it relies upon.

```py
# config/settings.py
INSTALLED_APPS = [
    
    'django.contrib.sites', # new
    'django.contrib.sitemaps', # new 

]

SITE_ID = 1 # new
```

- The sites framework requires an update to our database so run migrate at this time.
```py
python manage.py migrate
```

- The simplest approach is to use GenericSitemap, a convenience class that covers common sitemap usage.

```py
# config/urls.py
from django.contrib import admin
from django.contrib.sitemaps import GenericSitemap # new
from django.contrib.sitemaps.views import sitemap # new
from django.urls import path, include

urlpatterns = [
    path('sitemap.xml', sitemap, # new
        {'sitemaps': {'blog': GenericSitemap(info_dict, priority=0.6)}},
        name='django.contrib.sitemaps.views.sitemap'),
]
```

- Make sure the server is running and visit http://127.0.0.1:8000/sitemap.xml.

> It's also possible to change the priority and changefreq. And while you might notice that the current version uses http rather than https, if your production site uses https then that will be reflected in the sitemap. 

## Resources

- https://www.ordinarycoders.com/blog/article/django-sitemap
- https://medium.com/analytics-vidhya/django-sitemap-8f4ca0538fa

---
