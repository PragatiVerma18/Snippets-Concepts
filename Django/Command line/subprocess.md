# Subprocess Module in Python

> https://www.bogotobogo.com/python/python_subprocess_module.php

## `subprocess.Popen` vs `subprocess.call`
- `subprocess.Popen` is more general than `subprocess.call`.

- `Popen` **doesn't block**, allowing you to interact with the process while it's running, or continue with other things in your Python program. The call to `Popen` returns a `Popen` object.

- `call` **does block.** While it supports all the same arguments as the `Popen` constructor, so you can still set the process' output, environmental variables, etc., your script waits for the program to complete, and call returns a code representing the process' exit status.

```
returncode = call(*args, **kwargs) 
```
is basically the same as calling

```
returncode = Popen(*args, **kwargs).wait()
```

> Here is a rule of thumb:

- **call** is blocking:

```
call('notepad.exe')
print('hello')  # only executed when notepad is closed
```

- **Popen** is non-blocking:

```
Popen('notepad.exe')
print('hello')  # immediately executed
```

## `call_command` vs `subprocess.Popen`
- `call_command` is for calling Django management commands only - eg `syncdb`, `runserver`, or any custom management commands. *It calls the command directly, without shelling out to the system.*

- `popen` and the various functions in subprocess etc are *for shelling out to call any other executable file.*

---
