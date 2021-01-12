# Python

## Virtual environment

### Set up pyenv and pipenv

To set up a new python environment, first choose
which python version you want to use. To check
python versions:

    pyenv versions

If the python version you want to use is on the list,
continue, else:

    pyenv install 3.6.0

Now, while in new project directory, install python and
then pipenv:

    pyenv local 3.7.1
    pipenv --python 3.7.1

The environment will now run with that python version
and use pip in the folder's virtual environment

### Commands

    pyenv versions
    pyenv version

### Create New Environment

    pyenv virtualenv #{env name}

### Create new pipenv Environment

    pyenv install 3.6.5
    pyenv shell 3.6.5
    pip install pipenv
    cd /project_path
    pipenv --python 3.6.5

### Testing Email Energy

    python -m smtpd -n -c DebuggingServer localhost:1025
    
    
### Find Error Class
    try:
      something...
    except:
      print(sys.exc_info()[0])
      
      
### Call method with string variable
Assuming module foo with method bar:

    import foo
    str_var = 'bar'
    method_to_call = getattr(foo, str_var)
    result = method_to_call()
