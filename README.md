An exercise to develop a basic CRUD web application using React JS as frontend and Django Rest Framework for backend.

The outcome is to create a simple student management web application that looks like this:

//Image00

## Application Architecture

Here's the architecture of this simple Django web application:

![Architecture](/screenshots/01_Architecture.png)

The key operations of this application will be CRUD functions (Create,Read,Update,Delete), and implemented with REST APIs that use HTTP to communicate with programs over the web.

The basic HTTP verbs are POST, GET, PUT, PATCH and DELETE which correspond to create, read, update and delete respectively.


## Prep Backend Development

To develop the backend, I used [Pycharm](https://www.jetbrains.com/pycharm/download/#section=windows) and Django libraries.  

**Requirements:**  
Python==3.10
Django==4.1.1  
djangorestframework==3.14.0  
django-cors-headers==3.13.0

1. Open Pycharm and create a new project with a new virtual environment.
   
   ![PythonEnv](/screenshots/02_PythonEnv.png)

3. Open terminal and install required libraries inside virtual environment.
```
pip install Django==4.1.1
pip install djangorestframework==3.14.0
pip install django-cors-headers==3.13.0
```
   ![InstallLib](/screenshots/03_InstallLib.png)

3. Create a new Django project, which will auto generate some code e.g. django project structure, settings etc.
   
```
django-admin startproject backend
``` 
   ![BackEnd](/screenshots/04_BackendLib.png)

## Start Django Server

After the Django project is created, start the development server to check if project is initialized successfully.

Run this command to start Django development server
```
cd backend
python manage.py runserver
```
   ![StartDjango](/screenshots/05_StartDjangoServer.png)

The development server can now be accessed from web browser (http://127.0.0.1:8000/)

  ![DjangoServer](/screenshots/06_DjangoServer.png)


##  Create Students App
When you try to create an app, Django will automatically provision the directory structure.

Run the below command in the same directory where manage.py is:
```
python manage.py startapp students
```

Django will create the following files in students app directory:

![StudentsApp](/screenshots/07_StartAppStudents.png)

## Create Student Model
Then create a model for storing student information. A model is converted to database table after applying migrations.  
In the ```students/models.py``` file, add the below code to create Student model:

```
from django.db import models

class Student(models.Model):
    studentId = models.AutoField(primary_key=True)
    FirstName = models.CharField(max_length=100)
    LastName = models.CharField(max_length=100)
    RegistrationNo = models.CharField(max_length=100)
    Email = models.CharField(max_length=100)
    Course = models.CharField(max_length=100)
```
Django comes with a default SQLite database.
Next step will be to apply migrations to create Student table in the database.

Before running the migration, add students app in settings.py file.  
Open settings.py file and add students.apps.StudentsConfig to INSTALLED_APPS setting:
```
INSTALLED_APPS = [
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",
    "students.apps.StudentsConfig",
]
```

Now run this command to generate migrations script for students app.  
This will generate the script ```0001_initial.py``` inside ```students/migrations folder``` for all the models defined inside ```students/models.py```

```
python manage.py makemigrations students
```
![ApplyMigration](/screenshots/08_ApplyMigration.png)

Run this command to review the SQL generated for this migration:
```
python manage.py sqlmigrate students 0001
```
![CheckSQL](/screenshots/09_CheckSQL.png)


Now run migrate to create the student model in the database:
```
python manage.py migrate
```

##  Create Admin User
Next, create an admin user account to the admin site with this command:
```
python manage.py createsuperuser
```
Enter the username and password for the admin user.

Start the development server and go to (http://127.0.0.1:8000/admin/) to login with admin user account.
```
python manage.py runserver
```
![AdminLogin](/screenshots/10_AdminLogin.png)

After successful login, the Django admin page looks like this.
![AdminPage1](/screenshots/11_AdminPage.png)

Open ```students/admin.py``` and add below code in this file.
This will register the student model created earlier in the ```models.py``` file to the admin site.
```
from django.contrib import admin
from .models import Student

models_list = [Student]
admin.site.register(models_list)
```

Now refresh the admin page to see the changes:

![AdminPage2](/screenshots/12_AdminPage2.png)

