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

7. If you do not see any data, then make sure that backend service is up. To start the backend navigate to backend directory and start django server:

cd backend
python manage.py runserver

