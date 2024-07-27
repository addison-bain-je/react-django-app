An exercise to develop a basic CRUD web application using React JS as frontend and Django Rest Framework for backend.

The outcome is to create a simple student management web application that looks like this:

//Image01

## Application Architecture

Here's the architecture of this simple Django web application:

//Architecture Diagram

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
   
   //Image02

3. Open terminal and install required libraries inside virtual environment.
```
pip install Django==4.1.1
pip install djangorestframework==3.14.0
pip install django-cors-headers==3.13.0
```
 //Image03

3. Create a new Django project, which will auto generate some code e.g. django project structure, settings etc.
   //Image04
```
django-admin startproject backend
```

## Start Django Server

After the Django project is created, start the development server to check if project is initialized successfully.

Run this command to start Django development server
```
cd backend
python manage.py runserver
```

   //Image05

The development server can now be accessed from web browser (http://127.0.0.1:8000/)

  //Image06


