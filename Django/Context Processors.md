## Context processors
- A **context processor** has a simple interface: it’s a Python function that takes _one argument_, an _HttpRequest object_, and returns a dictionary that gets added to the template context.
- Each context processor **must return a dictionary**.
- Django projects are enabled with four context processors built-in to Django.
  - Django debug context processor
  - Django request context processor
  - Django auth context processor
  - Django messages context processor
- Other built-in Django context processors: **i18n, media, static, tz & CSRF context processors**

> Read more on [Built-in Context Processors](https://www.webforefront.com/django/usedefaultdjangocontextprocessors.html).

## Custom Context Processors

> **Most Important use case:** when the use case requires you to have the same data available across the entire application — by that, we mean across all templates of the application.

- Custom Django context processors allow you to set up data for access on all Django templates.
- Custom context processors can live anywhere in your codebase as long as they are pointed to by the context_processors argument of Engine.

> Read more on [Custom Context Processors](https://www.webforefront.com/django/setupdjangocontextprocessors.html).

---


