# Tools

We can use [pip](https://pip.pypa.io/en/stable/) \(python package installer\) to install packages. Also, it is common standard to use [virtualenv](https://virtualenv.pypa.io/en/latest/) to created isolated Python environment per project instead of using global  env. 

For packages dependency management pip uses `requirement.txt` file to hold current state/dependency but is not efficient for normal workflow. That's where `pipenv` comes to play.

#### Pipenv

[Pipenv](http://docs.pipenv.org/en/latest/) brings together pip, virtualenv and requirement \(better way\) to manage package. 

Pipenv uses `Pipfile` and `Pipfile.lock` to manage dependency.

#### Work-flow with pipenv: 

```bash
pip install pipenv

#runs "which python" cmd in virtual env and display path to virtual python executable
pipenv run which python

#ativates and changes current shell to virtual env
pipenv shell

cd my_project

#creates/install virtualenv and creates Pipfile and Pipfile.lock
pipenv install

#install the package and updates the Pipfile and Pipfile.lock with the dependency
pipenv install Django

#install dev env pacakges
pipenv install --dev Django

#uninstall the dependency
pipenv uninstall Django

#install the packages from Pipfiles
pipenv install
```

