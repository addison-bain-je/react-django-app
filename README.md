An exercise to develop a basic CRUD web application using React JS as frontend and Django Rest Framework for backend.

The outcome is to create a simple student management web application that looks like this:

![AppInterface](/screenshots/00_SampleReactApp.png)

# Application Architecture

Here's the architecture of this simple Django web application:

![Architecture](/screenshots/01_Architecture.png)

The key operations of this application will be CRUD functions (Create,Read,Update,Delete), and implemented with REST APIs that use HTTP to communicate with programs over the web.

The basic HTTP verbs are POST, GET, PUT, PATCH and DELETE which correspond to create, read, update and delete respectively.


# Backend Development

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


As super admin, you can add, delete, update student objects directly from admin panel into the database. However, we cannot expose the Django admin site to users or let them interact directly with the database.
Views must be created to handle user requests and perform basic CRUD operations with a proper application front-end.

## Create Student Serializer
Before creating a Student view, we need a serializer, so that complex data such as querysets and model instances can be converted to native Python datatypes that can then be easily rendered into JSON, XML or other content types.  
Serializers also provide deserialization, allowing parsed data to be converted back into complex types, after first validating the incoming data.

Create ```serializers.py``` file inside students directory. Open ```students/serializers.py``` and add below code in the Python file:
```
from rest_framework import serializers
from .models import Student

class StudentSerializer(serializers.ModelSerializer):
    class Meta:
        model = Student
        fields = ('studentId',
                  'FirstName',
                  'LastName',
                  'RegistrationNo',
                  'Email',
                  'Course')
```

## Create Student View  

Now write HTTP methods for GET, POST, PUT and DELETE to perform CRUD operation on the student model.
Open ```students/views.py``` and add below code in the file to support the creation of a new student record in Students table.

```
from django.http.response import Http404
from rest_framework.views import APIView
from rest_framework.response import Response
from django.http.response import JsonResponse
from .models import Student
from .serializers import StudentSerializer

class StudentView(APIView):

    def post(self, request):
        data = request.data
        serializer = StudentSerializer(data=data)

        if serializer.is_valid():
            serializer.save()
            return JsonResponse("Student Added Successfully",          safe=False)
        return JsonResponse("Failed to Add Student", safe=False)

```

To call this view, first map it to a URL — and so a URLconf is needed.

Create a file called ```urls.py``` in students directory.  
The directory structure should look like this:

![StudentDirectory](/screenshots/13_StudentDirectory.png)  

Open ```urls.py``` and below code in this file:
```
from django.urls import path
from .views import StudentView

urlpatterns = [
    path('students/', StudentView.as_view())
]
```

Next, include ```students/urls.py``` into root URLconf.  
Open ```backend/urls.py``` and include students.urls in urlpatterns list:
```
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path("admin/", admin.site.urls),
    path('', include('students.urls')),
]
```


Open ```backend/settings.py``` and include corsheaders and rest_framework apps in INSTALLED_APPS:
```
INSTALLED_APPS = [
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",
    "students.apps.StudentsConfig",
    'corsheaders',
    'rest_framework',
]
```

Go to (http://localhost:8000/students/) to see the Student Page on the browser.

![StudentView](/screenshots/14_StudentView01.png)  

Test POST Student API:
Send a Post request to the url (http://localhost:8000/students/).  
This will create a new student in the database table. Use the Django client or Postman to test the API call, by adding a similar payload to the post request:
```
{
"FirstName": "Addison",
"LastName": "Bain",
"RegistrationNo": "2023-CSE-01",
"Email": "addison.bain@student.com",
"Course": "Computer Science 101"
}
```

![StudentPost](/screenshots/15_StudentPost.png)  

## GET, PUT and DELETE Methods

Next, implement the other three methods for the app. (i.e. GET, PUT and DELETE to read, update and delete students)  
In the ```students/views.py``` file, add the remaining methods.

**GET**
```
def get_student(self, pk):
    try:
        student = Student.objects.get(studentId=pk)
        return student
    except Student.DoesNotExist:
        raise Http404

def get(self, request, pk=None):
    if pk:
        data = self.get_student(pk)
        serializer = StudentSerializer(data)
    else:
        data = Student.objects.all()
        serializer = StudentSerializer(data, many=True)
    return Response(serializer.data)
```

With this GET method above, it first checks if user has provided any student_id. 
If the student id is provided, then only one student with that id is retreived from the database. 
Otherwise all students will be retrieved and returned as JSON.

Refresh the url (http://127.0.0.1:8000/students/) to see all the student records in JSON format.
![StudentGetAll](/screenshots/16_StudentGet.png)  

To support retrieval of only one student record, make the following modifications:
Open ```students/urls.py``` and add the URL in urlpatterns list
```
path('students/<int:pk>/', StudentView.as_view())
```

The ```students/urls.py``` should look like this:
```
from django.urls import path
from .views import StudentView

urlpatterns = [
    path('students/', StudentView.as_view()),
    path('students/<int:pk>/', StudentView.as_view())
]
```
Now hit the URL again (http://127.0.0.1:8000/students/2) and you should be able to get the student record with id 2:
![StudentGetID](/screenshots/17_StudentGet2.png)  

**PUT**

In ```students/views.py``` add Put method to update a student record:
```
def put(self, request, pk=None):
    student_to_update = Student.objects.get(studentId=pk)
    serializer = StudentSerializer(instance=student_to_update, data=request.data, partial=True)

    if serializer.is_valid():
        serializer.save()
        return JsonResponse("Student updated Successfully", safe=False)
    return JsonResponse("Failed To Update Student")
```

**DELETE**

In ```students/views.py``` add delete method to delete a student record:

def delete(self, request, pk):
    student_to_delete = Student.objects.get(studentId=pk)
    student_to_delete.delete()
    return JsonResponse("Student Deleted Successfully", safe=False)



# Front End Development

## Prerequisites  
Check if NodeJS and npm are installed in your system. Run below in command prompt:

```
node --version
```
```
npm -version
```
![CheckNodeJS](/screenshots/18_CheckNodeNPM.png)
