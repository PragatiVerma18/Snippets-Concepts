# Django Signals
When saving data to a database, there are unique use cases where the business requirement of an application may require some processing just before or after saving the data. This means there should be a way to know when data is about to be saved or has just been saved in the database by the Django model method `save()`.

**Signals** are the components that work on the concept of senders and receivers. The **sending** component is usually the **model**, and the **receiving** component is usually the **processing function** that works on the data once it receives a notification that the data is just about to be saved or has just been saved.

## How it works?
- A **receiver** must be a function or an instance method which is to receive signals.
- A **sender** must either be a Python object, or None to receive events from any sender.
- The connection between the senders and the receivers is done through “signal dispatchers”, which are instances of Signal, via the connect method.
- The Django core also defines a `ModelSignal`, which is a subclass of Signal that allows the sender to be lazily specified as a string of the `app_label.ModelName` form. But, generally speaking, you will always want to use the Signal class to create custom signals.

> So to receive a signal, you need to register a receiver function that gets called when the signal is sent by using the `Signal.connect()` method.

### Resources
- [Introduction to Django Signals](https://www.pluralsight.com/guides/introduction-to-django-signals)
- [How to create Django Signals](https://simpleisbetterthancomplex.com/tutorial/2016/07/28/how-to-create-django-signals.html)

---
