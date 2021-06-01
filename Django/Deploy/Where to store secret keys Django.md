# Where to store secret keys Django?

So here's how I store my keys both **LOCALLY** and in **PRODUCTION (Heroku, and others)**.

**Note:** You really only have to do this if you plan on putting your project online. If it's just a local project, no need.

1) Install python-dotenv to create a local project environment to store your secret key.

```
pip install python-dotenv
```
2) Create a `.env` file in your base directory (where `manage.py` is).

```
YourDjangoProject
├───project
│   ├───__init__.py
│   ├───asgi.py
│   ├───settings.py
│   ├───urls.py
│   └───wsgi.py
├───.env
├───manage.py
└───db.sqlite3
```

If you have a Heroku project, it should look something like this:

```
YourDjangoProject
├───.git
├───project
│   ├───__init__.py
│   ├───asgi.py
│   ├───settings.py
│   ├───urls.py
│   └───wsgi.py
├───venv
├───.env
├───.gitignore
├───manage.py
├───Procfile
├───requirements.txt
└───runtime.txt
```

3) Add `.env` to your `.gitignore` file.

```
echo .env > .gitignore  # Or just open your .gitignore and type in .env
```

This is how you keep you're secret key more secure because you don't upload your `.env` file to git or heroku (or wherever else).

4) Add your `SECRET_KEY` from your settings.py file into the `.env` file like so (without quotes)

**Inside of your .env file**
```
SECRET_KEY=qolwvjicds5p53gvod1pyrz*%2uykjw&a^&c4moab!w=&16ou7 # <- Example key, SECRET_KEY=yoursecretkey
```

5) Inside of your `settings.py` file, add the following settings:

```
import os
import dotenv # <- New

```

# Add .env variables anywhere before SECRET_KEY

```
dotenv_file = os.path.join(BASE_DIR, ".env")
if os.path.isfile(dotenv_file):
    dotenv.load_dotenv(dotenv_file)
```

# UPDATE secret key

```
SECRET_KEY = os.environ['SECRET_KEY'] # Instead of your actual secret key
```

And now your secret key is successfully stored locally.

**Update:** I found out you can also use the config method from the package python-decouple that seems to be a bit easier:

```
from decouple import config

SECRET_KEY = config('SECRET_KEY')
```

Now you don't need to import os or use dotenv because it takes care of those parts for you AND will still use the `.env` file. 

6) Add the `SECRET_KEY` environment variable on your host (such as Heroku).

I work mostly with Heroku sites, so if you're wanting to use Heroku for a Django project, this part is for you.

This assumes that you already have a Heroku project setup and have Heroku CLI downloaded on your computer.

You have 2 options:

From Command Line / Terminal, you can enter the following command in your project's directory:
```
heroku config:set SECRET_KEY=yoursecretkey # Again, no quotes.
```
You can go to your Heroku dashboard, click on your app, go to your apps settings, and see the "Config Vars" section and click "Reveal Vars" or "Add Vars" and add your SECRET_KEY there.
Then, when you push your project to Heroku through git, it should be working properly without any issue.
