# Custom Django Management Commands
Django comes with a variety of command line utilities that can be either invoked using django-admin.py or the convenient manage.py script.
> A nice thing about it is that you can also add your own commands. It can also serve as an interface to execute cron jobs.

## Steps
- We can create our own commands for our apps and include them in the list by creating a `management/commands` directory inside an app directory.
- The name of the command file will be used to invoke using the command line utility. For example, if our command was called `my_custom_command.py`, then we will be able to execute it via:
```
python manage.py my_custom_command
```
- Basically a Django management command is composed by a class named `Command` which inherits from `BaseCommand`.
- The command code should be defined inside the `handle()` method.

**Quick Example:**

```py
# management/commands/what_time_is_it.py
# This command can be executed as:
# python manage.py what_time_is_it

from django.core.management.base import BaseCommand
from django.utils import timezone

class Command(BaseCommand):
    help = 'Displays current time'

    def handle(self, *args, **kwargs):
        time = timezone.now().strftime('%X')
        self.stdout.write("It's now %s" % time)
 ```
 
 ### How is that different from a regular Python script?
 The biggest benefit is that all Django tools are loaded and ready to use. That means you can import models, use Django's ORM to execute database queries, and interact with all of your project's resources.
 
### Resources
> [Simple is Better than Complex](https://simpleisbetterthancomplex.com/tutorial/2018/08/27/how-to-create-custom-django-management-commands.html#introduction)

---
