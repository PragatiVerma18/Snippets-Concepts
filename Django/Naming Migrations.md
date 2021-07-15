# Naming Migrations

Django came up with a name for the migration based on the timestamp—something like `0002_auto_20181112_1950`. If you’re not happy with that, then you can use the `--name` parameter to provide a custom name (without the `.py` extension).

To try that out, you first have to remove the old migration. You have already unapplied it, so you can safely delete the file:

```
$ rm historical_data/migrations/0002_auto_20181112_1950.py
```
Now you can recreate it with a more descriptive name:

```
$ ./manage.py makemigrations historical_data --name switch_to_decimals
```

This will create the same migration as before except with the new name of `0002_switch_to_decimals`.

---
