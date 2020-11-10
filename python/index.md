# Python

- **Flask**

  - Flask is built using two main frameworks: werkzeug and jinja2 (template engine);

  - A better way to work with flask is using factories

  - By convention, when we run `$ flash run` flask searches for a file called `app.py`. In case we want to change the main file, we must tell flask which files is the main file. To tell flask what files is the main file, run 
    `$ export FLASK_APP=another_main_file.py`

  - To run flask in development mode and get the pin code to debug the flask app in the browser we must export the `FLASK_ENV` var: `$ export FLASK_ENV=development` 

  - Commom errors:

    - **Circular Imports**: Avoid circular imports using factory methods. A very good practice is to wrap the creation of the flask app object in a function called `create_app` (by convention flask always looks for a function called `create app`)
      Example:

      ```python
      from flask import Flask
      
      def create_app():
      	app = Flask(__name__)
      	return app
      	
      ```

    - **Application out of context**: Flask has 3 main contexts: Config context, App context and request context. To avoid `application out of context` error we must know the life cycle of flask apps

- **WSGI**

  - WSGI stands for **W**eb **S**erver **G**ateway **I**nterface and it is a server application protocol. WSGI acts like a middleware which works between the Webserver(nginx, apache, IIS, etc) and the python application server (Gunicorn, Tornado, Twisted, etc)

  - To be able to implement the protocol and use it, it's necessary to implement a function that has two arguments `environ` and `start_response`, example:

    ```python
    def application(environ, start_response):
    	body = b'Hello World'
    	status = '200 OK'
    	headers = [('Content-type', 'text/html')]
    	start_response(status, headers)
    	return [body]
    ```

    To run with gunicorn:

    ```bash
    $ gunicorn app:application
    ```

- **setuptools**

  - The module setuptools (included in Python) has a function called `setup` that allows us to install our package/module using pip. It's important to provide a way to install our package/application, because it makes easy the process of install and test our package/application. In general, python projects use a file called `setup.py` to use the setup function. Example:

    ```python
    from setuptools import setup, find_packages 
    
    def function_to_read_from_requirements():
      return [requirement.strip() from requirement in open('requirements.txt').readlines()]
    
    setup(
    	name="appname",
      description="Description of the app name",
      version="0.1.0", # semantic versioning: major.minor.patch
      packages=find_packages(), # looks for packages/modules to install
      install_requirements=['package_required_by_our_app'],
      extras_require={
        "dev": function_to_read_from_requirements(),
        "prod": function_to_read_from_requirements()
      }
    )
    ```

    It's a  good practice to have two requirements.txt files: one for production and another for dev environment. 

    To run for dev env: `$ pip install -e . ['dev']`

    To run for production: `$ pip install -e . ['prod']` or `$ pip install -e .`

    To remove the app/package: `$ pip uninstall app_name`

    Another important thing to note is that function `find_packages` from setuptools looks for folders with a `__init__.py` file on it (python module).

- **Flask course link** (by Codeshow): [https://skip.gg/apostila-flask-python-codeshow](https://skip.gg/apostila-flask-python-codeshow) 

