# Logging
Logging is a technique or medium which can let us track some events as the software executes. It is an important technique for developers.
- The logging is handled by a separate program. That logging program is simply a file-writer.
- The logger is said to record certain events in text format.
- The recorded information is then saved in files. The files for this are called logs.
- The logs are simple files saved with log extension. They contain the logs of events occurred.

## Logging Module in Python
The logging module is a built-in Python module. It comes preinstalled with Python 3. 

### Why not print() rather than log?
We use print function to output something on console. So, when a function occurs, we can get a print statement that the function executed. While that approach works with smaller applications, it is inefficient. Print function becomes part of your program and if the software stops working, you won’t get the result. Also, if anything occurs and system restarts, the console is also clear.

The logging module is capable of:

- Multithreading execution
- Categorizing Messages via different log levels
- It’s much more flexible and configurable
- Gives a more structured information

## Understanding parts of logging module
There are 4 main parts of logging module:

### Loggers
They can be understood as a function which will be invoked when they are called. Thus, when the function is invoked, we get a detailed report.

### Handlers
- Handlers are the objects which emit the information.
- We can easily set-up multiple handlers for the same logger. 
- There are SMTP Handlers too which will mail the log records to you. 
> The handlers usually contain business logic for logging information.

### Formatters
- The formatters are the ones which format the data. 
- The logs are by-default in Log Records format. That is the class pre-defined by logging framework.
- That format can not be directly sent over a network or written in a text file. 
- To convert that or format that, we need formatters.
- By default, the formatters will convert the Log Record into String.

### Filters
Not every message we pass needs to be stored or transported. Or there can be different handlers for different messages. All that is achievable with the help of filters.
> We can use filters with both loggers and handlers.

## Logging Levels
**DEBUG:** It is verbose system information when everything is running fine. It will tell you more precise details about the state of the system. Its severity point is **10**.

**INFO:** The info will produce less verbose system information but is similar to debug. It generally tells an overview of what the system is executing. Its severity point is **20**.

**WARNING:** This contains information regarding low-level problems. The problems may be ignored as they don’t cause the system to halt. Although, it is recommended that these problems shall be resolved.

Its severity point is **30**.

**ERROR:** This message is serious. The error will contain information about the major problem that has occurred. The problem may have stopped the operation of program and needs immediate attention.

Its severity point is **40**.

**CRITICAL:** The most critical message. This message is emitted when the problem has caused the system to stop. That means the whole application has halted due to this problem.

Its severity point is **50**.

> The severity point determines what priority shall be given. The logger will log or store the information when the level is greater than or equal to the log level.

### Resources for Django
- https://djangodeconstructed.com/2018/12/18/django-and-python-logging-in-plain-english/#configure-logging
- https://data-flair.training/blogs/django-logging/
- https://coralogix.com/blog/python-logging-best-practices-tips/
- https://fangpenlin.com/posts/2012/08/26/good-logging-practice-in-python/
- https://www.webforefront.com/django/setupdjangologging.html#listing-5-15

----

