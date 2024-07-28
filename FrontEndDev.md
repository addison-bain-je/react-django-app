# Front End Development

## Create React App

1. Run this command in the terminal to create React app under the existing Pycharm project
```
npx create-react-app frontend
```
It may take some time to complete. The directory structure should look like this after the app is created:

![DirectoryFE](/screenshots/19_DirectoryFrontend.png)

2. Navigate to frontend directory:
```
cd frontend
```

3. Run npm start to start the react app:
```
npm start
```
This will start the app in the browser (http://localhost:3000/)

![CheckReact](/screenshots/20_CheckReact.png)

4. Remove the Starter code files inside src/ folder except ```index.js``` and ```reportWebVitals.jsf``` files.
  
5. Add a file named index.css in ```src/``` folder with the following CSS code:
```
body {
  font: 14px "Century Gothic", Futura, sans-serif;
  margin: 0;
}
```

6. Review the ```index.js``` file code
   This index.js file is the starting point of the app.
```
import App from './App';
import reportWebVitals from './reportWebVitals';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();
```

7. Add a file named ```App.js``` in the src/ folder with this JSX code:
```
import React from 'react';

function App() {
  return (
    <h1> Student Management System App </h1>
  );
}

export default App;
```

Now run ```npm start``` in the terminal again to see the header shown.

![CheckReactApp](/screenshots/21_CheckReactApp.png)

Next step is to create React components for Home, Navigation Bar, Students list and Manage Students page.

Create a new directory named ```components``` inside src/ folder. The current directory structure will look like this.

![DirectoryComponents](/screenshots/22_DirectoryComponents.png)


## Create TOP Navigation Bar 

1. Write the code to display a top Navigation bar which will remain static across all pages.

Add **react-bootstrap** to the project by running these commands inside frontend folder:
```
npm install bootstrap
npm install react-bootstrap
```
This will add bootstrap and react-bootstrap dependencies inside package.json file.


2. Next add some styling to set the width and height of the page at 100% and also add some padding for the logo.

Add a file named App.css in the src/ folder with this code:
```
body, html {
  height: 100%;
  width: 100%;
  margin: 0;
}

.app-logo {
   padding-left: 50px;
}
```

3. Put all the images and logo files inside static folder. Create a folder named ```static``` in the src/ folder and add ```logo.png``` file in this folder.

4. Add a file named Navigation.js in the src/components/ folder with this code:
```
import React from 'react';
import {Navbar,Nav} from 'react-bootstrap';
import logo from '../static/logo.png'
import "../App.css";


const Navigation = () => {
  return (
    <div>
    <Navbar bg="dark" variant="dark" expand="lg" id="my-nav">
        <Navbar.Brand className="app-logo" href="/">
            <img
              src={logo}
              width="50"
              height="50"
              className="d-inline-block align-center"
              alt="React Bootstrap logo"
            />{' '}
            Student Management System App
        </Navbar.Brand>
    </Navbar>
    </div>
  );
};

export default Navigation;
```

To render each component we need to add this inside the ```App.js``` file.

4. Add these lines below to the ```src/App.js``` file:
```
import React from 'react';
import 'bootstrap/dist/css/bootstrap.min.css';
import Navigation from "./components/Navigation";
```

This is to import bootstrap styling and Navigation component from ```components``` folder into ```App.js```.


5. Add below code in ```src/App.js``` to render Navigation component:
```
function App() {
  return (
      <Navigation />
  );
}

export default App;
```

Refresh the browser and the screen should look like this now:

![NavBar](/screenshots/23_ReactAppHeader.png)


## Create Side Navigation Bar

1. For side navigation bar we will use ```cdbreact``` library.
   Install this library using below command:
```npm install cdbreact``` 

3. Import ```NavLink``` and ```cdbreact``` components inside ```src/components/Navigation.js```.
   ```NavLink``` helps to navigate to different pages e.g Home, Students List or Manage students and ```cdbreact``` will create Sidebar.
```
import {NavLink} from 'react-router-dom';
import {
  CDBSidebar,
  CDBSidebarContent,
  CDBSidebarFooter,
  CDBSidebarHeader,
  CDBSidebarMenu,
  CDBSidebarMenuItem,
} from 'cdbreact';
```

3. Add code for sidebar in ```Navigation.js``` file below line ```</Navbar>```
```
<div className='sidebar'>
<CDBSidebar textColor="#333" backgroundColor="#f0f0f0">
    <CDBSidebarHeader prefix={<i className="fa fa-bars" />}>
      Navigation
    </CDBSidebarHeader>
    <CDBSidebarContent>
      <CDBSidebarMenu>
        <NavLink exact to="/" activeClassName="activeClicked">
          <CDBSidebarMenuItem icon="home">Home</CDBSidebarMenuItem>
        </NavLink>
        <NavLink exact to="/student" activeClassName="activeClicked">
          <CDBSidebarMenuItem icon="list">Students List</CDBSidebarMenuItem>
        </NavLink>
        <NavLink exact to="/manage" activeClassName="activeClicked">
          <CDBSidebarMenuItem icon="user">Manage Students</CDBSidebarMenuItem>
        </NavLink>
      </CDBSidebarMenu>
    </CDBSidebarContent>
  </CDBSidebar>
</div>
```


The final ```Navigation.js``` file should look like this:
```
import React from 'react';
import {
  CDBSidebar,
  CDBSidebarContent,
  CDBSidebarHeader,
  CDBSidebarMenu,
  CDBSidebarMenuItem,
} from 'cdbreact';
import {NavLink} from 'react-router-dom';
import {Navbar} from 'react-bootstrap';
import logo from '../static/logo.png';
import "../App.css";


const Navigation = () => {
  return (
    <div>
    <Navbar bg="dark" variant="dark" expand="lg" id="my-nav">
        <Navbar.Brand className="app-logo" href="/">
            <img
              src={logo}
              width="40"
              height="50"
              className="d-inline-block align-center"
              alt="React Bootstrap logo"
            />{' '}
            Student Management System
        </Navbar.Brand>
    </Navbar>
    <div className='sidebar'>
    <CDBSidebar textColor="#333" backgroundColor="#f0f0f0">
        <CDBSidebarHeader prefix={<i className="fa fa-bars" />}>
          Navigation
        </CDBSidebarHeader>
        <CDBSidebarContent>
          <CDBSidebarMenu>
            <NavLink exact to="/" activeClassName="activeClicked">
              <CDBSidebarMenuItem icon="home">Home</CDBSidebarMenuItem>
            </NavLink>
            <NavLink exact to="/students" activeClassName="activeClicked">
              <CDBSidebarMenuItem icon="list">Students List</CDBSidebarMenuItem>
            </NavLink>
            <NavLink exact to="/manage" activeClassName="activeClicked">
              <CDBSidebarMenuItem icon="user">Manage Students</CDBSidebarMenuItem>
            </NavLink>
          </CDBSidebarMenu>
        </CDBSidebarContent>
      </CDBSidebar>
    </div>
    </div>
  );
};

export default Navigation;
```

4. This side nav bar will be defined by adding className='sidebar' inside the ```src/App.css``` file:
```
.sidebar {
   display: flex;
   height: 100vh;
   float: left;
   overflow: 'scroll initial';
}
```

5. For ```NavLink``` to function, import ```BrowserRouter``` component to the ```src/App.js``` file:
```
import {BrowserRouter} from 'react-router-dom';
```

6. Update function ```App()``` code in ```App.js```:
```
function App() {
  return (
    <BrowserRouter>
      <Navigation />
    </BrowserRouter>
  );
}
```

7. After refreshing the page, the side navigation bar should appear:
![SideBar](/screenshots/24_ReactAppSideBar.png)

## Create Home Page  
Create a home page with a simple image slider. For image slider, use **react-bootstrap** ```Carousel```component.

1. Add a file named ```Home.js``` inside /src/components folder with this code:
```
import slide01 from '../static/slide01.jpg'
import slide02 from '../static/slide02.jpg'
import slide03 from '../static/slide03.jpg'

import Carousel from 'react-bootstrap/Carousel';

const Home = () => {
  return (
  <div className="row">
    <Carousel variant="dark">
      <Carousel.Item>
        <img
          className="d-block w-100"
          src={slide01}
          alt="First slide"
        />
      </Carousel.Item>
      <Carousel.Item>
        <img
          className="d-block w-100"
          src={slide03}
          alt="Second slide"
        />
      </Carousel.Item>
      <Carousel.Item>
        <img
          className="d-block w-100"
          src={slide02}
          alt="Third slide"
        />
      </Carousel.Item>
    </Carousel>
    </div>
  );
};

export default Home;
```

2. Add files slide01.jpg, slide02.jpg and slide03.jpg inside ```/src/static``` folder.

3. Then add ```Home``` component inside ```App.js``` file for this to render. Before that, install ```react-router library``` to route to different pages.
```
npm install react-router
npm install react-router-dom
```

4. Add Home component as a Route inside ```App.js``` file:
```
import Home from "./components/Home";
import {BrowserRouter, Route, Routes} from 'react-router-dom';
function App() {
  return (
    <BrowserRouter>
      <Navigation />
      <Routes>
         <Route exact path="/" element={<Home/>} />
       </Routes>
    </BrowserRouter>
  );
}
```

5. Execute ```npm start``` and refresh the page, it should look like this:

![HomePage](/screenshots/25_ReactAppHomePage.png)


The Students List or Manage Students pages are still empty. Let's develop these pages next.

## Create Students List Page
Get the students list via the backend API that was developed with Django.  
To call the API from React, create a StudentService.

1. Create a folder named ```services``` inside ```/srcfolder``` and add a file named ```StudentService.js``` inside ```/src/services``` folder with this code:
```
import axios from 'axios';

export function getStudents() {
  return axios.get('http://127.0.0.1:8000/students/')
    .then(response => response.data)
}
```

This creates a function ```getStudents()``` which calls backend API endpoint ```/students``` to fetch a list of students from the database. We need to use the ```axios library``` for this. Install this library using this command:
```
npm install axios
```

2. Add styling to this component inside App.css file:
```
.side-container {
   padding-top: 30px;
}

.side-row {
   padding: 30px;
}

.react-bootstrap-table thead { 
    position: sticky; 
    top: 0; 
    background-color: #333; 
    z-index: 1021; 
    color: white; 
}
```

3. Add a file named ```Students.js``` inside ```/src/components``` folder with below code:
```
import React, { useEffect, useState } from 'react';
import { Table } from 'react-bootstrap';
import { getStudents } from '../services/StudentService';
import "../App.css";

const Students = () => {
  const [students, setStudents] = useState([]);

  useEffect(() => {
   let mounted = true;
   getStudents()
     .then(data => {
       if(mounted) {
         setStudents(data)
       }
     })
   return () => mounted = false;
 }, [])

  return(
   <div className="container-fluid side-container">
   <div className="row side-row" >
    <p id="before-table"></p>
        <Table striped bordered hover className="react-bootstrap-table" id="dataTable">
        <thead>
            <tr>
            <th>ID</th>
            <th>First Name</th>
            <th>Last Name</th>
            <th>Registration No</th>
            <th>Email</th>
            <th>Course</th>
            </tr>
        </thead>
        <tbody>
            {students.map((stu) =>
            <tr key={stu.id}>
                <td>{stu.studentId}</td>
                <td>{stu.FirstName}</td>
                <td>{stu.LastName}</td>
                <td>{stu.RegistrationNo}</td>
                <td>{stu.Email}</td>
                <td>{stu.Course}</td>
            </tr>)}
        </tbody>
    </Table>
    </div>
  </div>
  );
};

export default Students;
```

Everytime the page is refreshed or loaded, ```useEffect``` hook will call the ```getStudents``` service that is defined inside ```StudentService.js``` file.

4. Finally, add a route for Students component inside ```App.js```:
```
import Students from "./components/Students";
function App() {
  return (
    <BrowserRouter>
      <Navigation />
      <Routes>
         <Route exact path="/" element={<Home/>} />
         <Route path="/students" element={<Students/>} />
       </Routes>
    </BrowserRouter>
  );
}
```

5. Refresh the React page and navigate to Students List page to get the data from backend.
   Make sure the Django server is up first.
```
cd backend
python manage.py runserver
```

## Cross-Origin Resource Sharing  
If the Student list does not load or some error messages appear, it is probably due to ```Cross-Origin Resource Sharing``` not allowed by backend server. In that case ```AllowOrigin header``` is usually missing in the response. To allow Javascript to read response data from API, ```Cross-Origin Resource Sharing``` must be allowed by the backend server.  

In ```backend/settings.py``` file, check for the following:

i) Check if ```’corsheaders'``` is added in ```INSTALLED_APPS```:
```
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'backend',
    'corsheaders',
    'rest_framework',
]
```

ii) Check if ```CORS_ORIGIN_ALLOW_ALL = True``` is set:
```
CORS_ORIGIN_ALLOW_ALL = True
```

iii) Check if ```'corsheaders.middleware.CorsMiddleware'``` is added in MIDDLEWARE:
```
CORS_ORIGIN_ALLOW_ALL = True

MIDDLEWARE = [
    'corsheaders.middleware.CorsMiddleware',
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]
```

Refresh the Students page again and the data should be loaded onto the view.
![StudentView](/screenshots/26_ReactAppStudentsList.png)


## Create Manage Students Page
Now develop the functionalities to add student, update student and delete student. Separate components will be used for these. Install ```react-icons``` library to use delete and update icons from this library.
```
npm install react-icons
```

**Create Manage.js**  
1. Add a file named ```Manage.js``` in ```/src/components``` folder
  
2. Add these imports in ```Manage.js``` file:
```
import React,{ useEffect, useState } from 'react';
import {Table} from 'react-bootstrap';

import {Button,ButtonToolbar } from 'react-bootstrap';
import { FaEdit } from 'react-icons/fa';
import { RiDeleteBin5Line } from 'react-icons/ri';
import { getStudents, deleteStudent } from '../services/StudentService';
import AddStudentModal from "./AddStudentModal";
import UpdateStudentModal from "./UpdateStudentModal";
```

Use ```useState``` hook for managing states e.g. for updating students list when a new student is added or deleted.  
```useEffect``` state will be used for managing events e.g. updating page contents when a student is added or deleted.

Add components for ```AddStudentModal``` and ```updateStudentModal``` later.

3. Add these states in ```Manage.js``` file:
```
const Manage = () => {
    const [students, setStudents] = useState([]);
    const [addModalShow, setAddModalShow] = useState(false);
    const [editModalShow, setEditModalShow] = useState(false);
    const [editStudent, setEditStudent] = useState([]);
    const [isUpdated, setIsUpdated] = useState(false);
};
```

4. Add ```useEffect``` hook in ```Manage.js```:
```
useEffect(() => {
   let mounted = true;
   if(students.length && !isUpdated) {
    return;
    }
   getStudents()
     .then(data => {
       if(mounted) {
         setStudents(data);
       }
     })
   return () => {
      mounted = false;
      setIsUpdated(false);
   }
 }, [isUpdated, students])

export default Manage;
```

This hook checks if the students list is updated on backend due to any CRUD operation, which then updates the students state and re-render the updated list on the frontend.

5. Next, add handlers for handling update, add and delete events:
```
   const handleUpdate = (e, stu) => {
    e.preventDefault();
    setEditModalShow(true);
    setEditStudent(stu);
};
```

Here, when a user clicks on update button, call ```handleUpdate``` handler on button click event. This handler will set some states i.e. enable edit student form for editing student record.

Similarly, add the Add and Delete handlers:
```
const handleAdd = (e) => {
    e.preventDefault();
    setAddModalShow(true);
};

const handleDelete = (e, studentId) => {
    if(window.confirm('Are you sure ?')){
        e.preventDefault();
        deleteStudent(studentId)
        .then((result)=>{
            alert(result);
            setIsUpdated(true);
        },
        (error)=>{
            alert("Failed to Delete Student");
        })
    }
};
```

In ```handleDelete```, call the ```deleteStudent``` service which will be defined in ```/src/services/StudentService.js``` file:
```
export function deleteStudent(studentId) {
  return axios.delete('http://127.0.0.1:8000/students/' + studentId + '/', {
   method: 'DELETE',
   headers: {
     'Accept':'application/json',
     'Content-Type':'application/json'
   }
  })
  .then(response => response.data)
}
```

6. Finally, add bootstrap for rendering content on Manage students page on the ```Manage.js``` file:
```
let AddModelClose=()=>setAddModalShow(false);
let EditModelClose=()=>setEditModalShow(false);
return(
    <div className="container-fluid side-container">
    <div className="row side-row" >
    <p id="manage"></p>
        <Table striped bordered hover className="react-bootstrap-table" id="dataTable">
            <thead>
            <tr>
              <th >ID</th>
              <th>First Name</th>
              <th>Last Name</th>
              <th>Registration No</th>
              <th>Email</th>
              <th>Course</th>
              <th>Action</th>
            </tr>
            </thead>
            <tbody>
              { students.map((stu) =>

              <tr key={stu.id}>
              <td>{stu.studentId}</td>
              <td>{stu.FirstName}</td>
              <td>{stu.LastName}</td>
              <td>{stu.RegistrationNo}</td>
              <td>{stu.Email}</td>
              <td>{stu.Course}</td>
              <td>

              <Button className="mr-2" variant="danger"
                onClick={event => handleDelete(event,stu.studentId)}>
                    <RiDeleteBin5Line />
              </Button>
              <span>&nbsp;&nbsp;&nbsp;</span>
              <Button className="mr-2"
                onClick={event => handleUpdate(event,stu)}>
                    <FaEdit />
              </Button>
              <UpdateStudentModal show={editModalShow} student={editStudent} setUpdated={setIsUpdated}
                          onHide={EditModelClose}></UpdateStudentModal>
            </td>
            </tr>)}
          </tbody>
        </Table>
        <ButtonToolbar>
            <Button variant="primary" onClick={handleAdd}>
            Add Student
            </Button>
            <AddStudentModal show={addModalShow} setUpdated={setIsUpdated}
            onHide={AddModelClose}></AddStudentModal>
        </ButtonToolbar>
    </div>
    </div>
);
```

This code calls handlers on button click events e.g. ```handleUpdate``` and the logic to update/add students is being handled in ```UpdateStudentModal``` and ```AddStudentModal``` components which will be implemented below.

**AddStudentModal.js**

1. Add a file named ```AddStudentModal.js``` in ```/src/components``` with below code:
```
import React from 'react';
import {Modal, Col, Row, Form, Button} from 'react-bootstrap';
import {FormControl, FormGroup, FormLabel} from 'react-bootstrap';
import { addStudent } from '../services/StudentService';


const AddStudentModal = (props) => {

    const handleSubmit = (e) => {
        e.preventDefault();
        addStudent(e.target)
        .then((result)=>{
            alert(result);
            props.setUpdated(true);
        },
        (error)=>{
            alert("Failed to Add Student");
        })
    }

    return(
        <div className="container">

            <Modal
                {...props}
                size="lg"
                aria-labelledby="contained-modal-title-vcenter"
                centered >

                <Modal.Header closeButton>
                    <Modal.Title id="contained-modal-title-vcenter">
                        Fill In Student Information
                    </Modal.Title>
                </Modal.Header>
                <Modal.Body>
                    <Row>
                        <Col sm={6}>
                            <Form onSubmit={handleSubmit}>
                                <Form.Group controlId="FirstName">
                                    <Form.Label>First Name</Form.Label>
                                    <Form.Control type="text" name="FirstName" required placeholder="" />
                            </Form.Group>
                            <Form.Group controlId="LastName">
                                    <Form.Label>Last Name</Form.Label>
                                    <Form.Control type="text" name="LastName" required placeholder="" />
                            </Form.Group>
                            <Form.Group controlId="RegistrationNo">
                                    <Form.Label>Registration No.</Form.Label>
                                    <Form.Control type="text" name="RegistrationNo" required placeholder="" />
                            </Form.Group>
                            <Form.Group controlId="Email">
                                    <Form.Label>Email</Form.Label>
                                    <Form.Control type="text" name="Email" required placeholder="" />
                            </Form.Group>
                            <Form.Group controlId="Course">
                                    <Form.Label>Course</Form.Label>
                                    <Form.Control type="text" name="Course" required placeholder="" />
                            </Form.Group>
                            <Form.Group>
                                <p></p>
                                <Button variant="primary" type="submit">
                                    Submit
                                </Button>
                            </Form.Group>
                            </Form>
                        </Col>
                    </Row>
                </Modal.Body>
                <Modal.Footer>
                <Button variant="danger" type="submit" onClick={props.onHide}>
                        Close
                </Button>

                </Modal.Footer>
            </Modal>
        </div>
    );
};

export default AddStudentModal;
```

Props are used for passing states information from one component to other. In this case, for passing students information from ```Manage.js``` into ```AddStudentModal``` component.

```handleSubmit``` handler will be called once user clicks submit button. This handler will call ```addStudent``` service which uses the backend endpoint to add student in database.

2. Add ```addStudent``` service in ```/src/services/StudentService.js``` :
```
export function addStudent(student){
  return axios.post('http://127.0.0.1:8000/students/', {
    studentId:null,
    FirstName:student.FirstName.value,
    LastName:student.LastName.value,
    RegistrationNo:student.RegistrationNo.value,
    Email:student.Email.value,
    Course:student.Course.value
  })
    .then(response=>response.data)
}
```

**UpdateStudentModal.js**  
1. Add a file named ```UpdateStudentModal.js``` in ```/src/components``` with below code:
```
import React,{Component} from 'react';
import {Modal, Col, Row, Form, Button} from 'react-bootstrap';
import {FormControl, FormGroup, FormLabel} from 'react-bootstrap';
import { updateStudent } from '../services/StudentService';

const UpdateStudentModal = (props) => {

    const handleSubmit = (e) => {
        e.preventDefault();
        updateStudent(props.student.studentId, e.target)
        .then((result)=>{
            alert(result);
            props.setUpdated(true);
        },
        (error)=>{
            alert("Failed to Update Student");
        })
    };

    return(
        <div className="container">

            <Modal
                {...props}
                size="lg"
                aria-labelledby="contained-modal-title-vcenter"
                centered >

                <Modal.Header closeButton>
                    <Modal.Title id="contained-modal-title-vcenter">
                        Update Student Information
                    </Modal.Title>
                </Modal.Header>
                <Modal.Body>
                    <Row>
                        <Col sm={6}>
                            <Form onSubmit={handleSubmit}>
                                <Form.Group controlId="FirstName">
                                    <Form.Label>First Name</Form.Label>
                                    <Form.Control type="text" name="FirstName" required defaultValue={props.student.FirstName} placeholder="" />
                            </Form.Group>

                            <Form.Group controlId="LastName">
                                    <Form.Label>Last Name</Form.Label>
                                    <Form.Control type="text" name="LastName" required defaultValue={props.student.LastName} placeholder="" />
                            </Form.Group>
                            <Form.Group controlId="RegistrationNo">
                                    <Form.Label>Registration No.</Form.Label>
                                    <Form.Control type="text" name="RegistrationNo" required defaultValue={props.student.RegistrationNo} placeholder="" />
                            </Form.Group>
                            <Form.Group controlId="Email">
                                    <Form.Label>Email</Form.Label>
                                    <Form.Control type="text" name="Email" required defaultValue={props.student.Email} placeholder="" />
                            </Form.Group>
                            <Form.Group controlId="Course">
                                    <Form.Label>Course</Form.Label>
                                    <Form.Control type="text" name="Course" required defaultValue={props.student.Course} placeholder="" />
                            </Form.Group>
                            <Form.Group>
                                <p></p>
                                <Button variant="primary" type="submit">
                                    Submit
                                </Button>
                            </Form.Group>
                            </Form>
                        </Col>
                    </Row>
                </Modal.Body>
                <Modal.Footer>
                <Button variant="danger" type="submit" onClick={props.onHide}>
                        Close
                </Button>

                </Modal.Footer>
            </Modal>
        </div>
    );
};

export default UpdateStudentModal;
```

2. Add ```updateStudent``` service in ```/src/services/StudentService.js``` :
```
export function updateStudent(stuid, student) {
  return axios.put('http://127.0.0.1:8000/students/' + stuid + '/', {
    FirstName:student.FirstName.value,
    LastName:student.LastName.value,
    RegistrationNo:student.RegistrationNo.value,
    Email:student.Email.value,
    Course:student.Course.value
  })
   .then(response => response.data)
}
```

**Add Manage component in React Router**  
1. To render ```Manage``` component, add this as a Route in ```/src/App.js```:
```
import Manage from "./components/Manage";
function App() {
  return (
    <BrowserRouter>
      <Navigation />
      <Routes>
         <Route exact path="/" element={<Home/>} />
         <Route path="/students" element={<Students/>} />
         <Route path="/manage" element={<Manage/>} />
       </Routes>
    </BrowserRouter>
  );
};
```

## Test CRUD Operations  

1. Navigate to Manage Students page. It should look like this:
![ReactStudentPage](/screenshots/27_ManageStudents.png)

2. Click on Add Student button to open up a blank student form.
![AddStudent](/screenshots/28_AddStudent.png)

3. Fill in the student information and click submit. This will open a popup alert if student record is created successfully:
![AddStudentSuccess](/screenshots/29_AddStudentSuccess.png)

4. After closing the student form, notice that the students list is updated without refreshing the page. The ```useEffect``` hook helps to refresh the list automatically whenever a student record is created, deleted or updated.
![ManageStudent](/screenshots/30_ManageStudentUpdated.png)

5. Similarly, test out the Update and Delete operations.


---------------------------------------------------- END ----------------------------------------------------
   


