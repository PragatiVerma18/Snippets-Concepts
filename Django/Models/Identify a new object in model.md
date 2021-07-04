# In a django model custom save() method, how should you identify a new object?

- We can check self._state of the model

`self._state.adding` is _True_ - **creating**

`self._state.adding` is _False_ - **updating**

> Read more [here](https://docs.djangoproject.com/en/dev/ref/models/instances/#customizing-model-loading)

- Checking `self.id` assumes that id is the primary key for the model. A more generic way would be to use the [pk shortcut](http://docs.djangoproject.com/en/dev/topics/db/queries/#the-pk-lookup-shortcut).

```py
is_new = self.pk is None
```
---

# Get current user in model save

I found a way to do that, it involves declaring a MiddleWare, though. Create a file called `get_username.py` inside your app, with this content:
```py
from threading import current_thread

from django.utils.deprecation import MiddlewareMixin


_requests = {}


def get_username():
    return _requests.get(current_thread().ident, None)


class RequestMiddleware(MiddlewareMixin):
    def process_request(self, request):
        _requests[current_thread().ident] = request

    def process_response(self, request, response):
        # when response is ready, request should be flushed
        _requests.pop(current_thread().ident, None)
        return response

    def process_exception(self, request, exception):
        # if an exception has happened, request should be flushed too
        _requests.pop(current_thread().ident, None)

```

Edit your `settings.py` and add it to the `MIDDLEWARE_CLASSES`:

```py
    MIDDLEWARE_CLASSES = (
        ...
        'yourapp.get_username.RequestMiddleware',
    )
```

Now, in your `save()` method, you can get the current username like this:
```py
    from get_username import get_username
    
    ...
    
    def save(self, *args, **kwargs):
        req = get_username()
        print "Your username is: %s" % (req.user)
```

> Read more [here](https://stackoverflow.com/questions/10991460/django-get-current-user-in-model-save)
---
