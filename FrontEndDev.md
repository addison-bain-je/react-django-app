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
   
