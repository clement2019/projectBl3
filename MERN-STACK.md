## SIMPLE TODO APPLICATION ON MERN WEB STACK

The projects shows an interface popularly called GUI where a user interacts with the ReactJS UI components
at the software front-end residing in the browser. This frontend is served by the software backend residing in a server,
through ExpressJS running on top of NodeJS. Any interaction or data change request is sent to the NodeJS based Express server,
which collects data from the MongoDB database if required, and returns the data to the frontend of the application,
which is then presented to the user consumption.

          The following processes describes the 

   TASK TO DEPLOY A SIMPLE TO DO LIST APPLICATION

   I started this project by first creating a MERN-stack web server in Aws in my availability zone eu-west 2a,
   
   configured the security group with the necessary configuration settings SSH on port:22 , HTTP on port :80 , customer TCP on port:5000
   
   and another customer TCP on port:3000 thereby creating the necessity FIREWALL.I created my private key to be able to connect 
   
   to my EC2 instance and with the help of the key i was able to use (SSH client) connection to connect to my instance
   
   using Gitbash installed on my machine

INSTALLING THE NGINX WEB SERVER

updated my machine by running

![image](https://user-images.githubusercontent.com/55473846/139442133-3e307b51-9fda-4b57-8c61-eddc5829ffad.png)

sudo apt update

![image](https://user-images.githubusercontent.com/55473846/139443518-5735bca3-faf9-4e1d-92da-48fa96a74358.png)

To get the location of Node.js software from Ubuntu repositories, i ran

curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash 

NOW INSTALL THE NODE.JS ON THE SERVER

There are so many packages to be installed for any software to work better while npm package manager is used for the Nodes application,

install Node modules & packages and To manage dependency conflicts, while the apt is used for ubuntu node like apt for ubuntu the

command below installs both nodejs and npm, while npm is a package manager.Verify the node installation with the command below

sudo apt-get install -y nodejs

node -v

![image](https://user-images.githubusercontent.com/55473846/139443818-23da0184-74b4-429a-9f83-a889e94122ef.png)

APPLICATION CODE SETUP

I created a new directory for my To-Do project:

mkdir Todo

I ran this command below to verify that the Todo directory is created with ls command

![image](https://user-images.githubusercontent.com/55473846/139444174-058ffd92-f6e5-451e-92a6-22d2f688cb8d.png)

However, for me to see more useful information about files and directories, i can the following combination of keys ls -lih

![image](https://user-images.githubusercontent.com/55473846/139445357-d65d775c-29f2-449b-8828-1cc3f04ad8fa.png)

Because all my application files need to be in one central location folder I now changed my current directory to the newly

created one as shown below

cd Todo

As usual at the beginning of any project, I use the command npm init to initialize my project packages, 

so that a new file named package.json will be created.

This file will normally contain information about the software and its dependencies that it needs to run. Following the prompts 

after running the command i hit on Enter several times to accept default values, then yes to accept to write out the package.json file.

npm init

![image](https://user-images.githubusercontent.com/55473846/139445873-a9b044c2-0efa-409d-97c3-e4f8c60bc80c.png)

There is need to confirm that the package has been configured or created so i ran the command ls to confirm that i had package.json file 
created,
Next, i installed ExpressJs and created the Routes directory.

INSTALL EXPRESSJS

Its nice to see that at this stage i can now install Express which is a framework for Node.js, meaning that most of the thing’s developers

might have chosen to develop or programed are already in the framework for our own usage and is now taken care of for us.

This allows for simplicity in the development processes 

and workflow as a lot of low-level details have been embedded in the library.

A typical example of such scenario is where Express assist in defining routes of our software based on HTTP methods and URLs 

 To use express, I installed it using npm

![image](https://user-images.githubusercontent.com/55473846/139446756-c2b8544f-09b2-4d28-86dd-9548e384a051.png)

I created a file in this directory and name it index.js with command below

touch index.js

Ran ls to confirm that the index.js file is successfully created

Install the dotenv module

npm install dotenv

![image](https://user-images.githubusercontent.com/55473846/139447067-b28144aa-8acf-433c-9333-13715601c087.png)

I now pasted the code below into the index.js file 

const express = require('express');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

app.use((req, res, next) => {
res.header("Access-Control-Allow-Origin", "\*");
res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
next();
});

app.use((req, res, next) => {
res.send('Welcome to Express');
});

app.listen(port, () => {
console.log(`Server running on port ${port}`)
});

The content of index.js is as shown below in the screenshot:

![image](https://user-images.githubusercontent.com/55473846/139447338-a56ec77a-753d-453e-8948-03610413f69f.png)

I started the server to see if all is good and opened the terminal in the same directory as the index.js file

I ran the command below to check if server default page is running

node index.js

I started the server to see if all is good and opened the terminal in the same directory as the index.js file

I ran the command below to check if server default page is running

node index.js

![image](https://user-images.githubusercontent.com/55473846/139447671-e3a2bf28-c8b5-4311-9011-d1a2af8e9ccf.png)

In project 2 LEMP-STACK project I opened port:3000 on the security group, i installed NGINX server and

we latter edited inbound rule to open custom TCP on port:5000 as shown below: 

![image](https://user-images.githubusercontent.com/55473846/139449817-c10283ac-6537-4832-a0ef-f87b9d3a6501.png)

AFTER RUNNING

http://ec2-18-132-203-54.eu-west-2.compute.amazonaws.com:5000/

![image](https://user-images.githubusercontent.com/55473846/139451111-d10526af-16d2-43b5-82db-f48bfd773301.png)

Now we need to create the Routes for the To Do application

Routes

There are three actions that our To-Do application needs to be able to do:

1.	Create a new task
2.	Display list of all tasks
3.	Delete a completed task

Each task will be associated with some particular endpoint and will use different standard HTTP request methods: POST, GET, DELETE.

For each task, we need to create routes that will define various endpoints that the To-do app will depend on. So i created a folder routes

mkdir routes

using my ec2 instance to connect using my Gitbash

Change directory to routes folder.

![image](https://user-images.githubusercontent.com/55473846/139451427-92b67fa3-ba9e-4978-be4b-513a5dd1b95c.png)

Now we created a file api.js with the command below

touch api.js

Open the file with the command below

vim api.js

![image](https://user-images.githubusercontent.com/55473846/139451605-f2ce75f9-a1f8-4294-a1f0-0c8e962e7f28.png)

Moving forward l created Models directory.

MODELS

Now comes the exciting part, since the app is going to make use of Mongodb which is a NoSQL database, I needed to create a model.

A model is at the heart of JavaScript based applications, and it is what makes it interactive.

I also made use models to define the database schema. This is important so that i will be able to define the fields stored in 
each Mongodb document
To create a Schema and a model i installed mongoose which is a Node.js package that makes working with mongodb easier.

I Changed directory back Todo folder with cd .. and install Mongoose

npm install mongoose

![image](https://user-images.githubusercontent.com/55473846/139451942-dd635c79-ca8d-4db9-9665-806f1ef0871d.png)

Create a new folder models:

mkdir models

Change directory into the newly created ‘models’ folder with

cd models

Inside the model’s folder, create a file and name it todo.js

touch todo.js

![image](https://user-images.githubusercontent.com/55473846/139452111-0afc3080-df9e-4e61-be2d-734200b00264.png)

I updated our routes from the file api.js in ‘routes’ directory to make use of the new model.

In Routes directory, i opened api.js with vim api.js, delete the code inside with :%d command and paste there code below into

it then save and exit

const express = require ('express');
const router = express.Router();
const Todo = require('../models/todo');

router.get('/todos', (req, res, next) => {

//this will return all the data, exposing only the id and action field to the client
Todo.find({}, 'action')
.then(data => res.json(data))
.catch(next)
});

router.post('/todos', (req, res, next) => {
if(req.body.action){
Todo.create(req.body)
.then(data => res.json(data))
.catch(next)
}else {
res.json({
error: "The input field is empty"
})
}
});

router.delete('/todos/:id', (req, res, next) => {
Todo.findOneAndDelete({"_id": req.params.id})
.then(data => res.json(data))
.catch(next)
})

module.exports = router;

![image](https://user-images.githubusercontent.com/55473846/139452381-92c7e3d6-3d4c-41cf-a76c-a05064e06405.png)

The next piece of our application will be the MongoDB Database

MONGODB DATABASE

I needed a database where i will store my application data written in applicationjson format. For this i registered an account with MongoDB and signed up

for a shared clusters free account, which is ideal for our what i want to do.

I signed up and follow the sign up process, select AWS as the cloud provider of choice, and choose a region near me. 

npm install mongoose

![image](https://user-images.githubusercontent.com/55473846/139452766-55f8405b-91fe-4e50-bb30-a32235b3f26f.png)

![image](https://user-images.githubusercontent.com/55473846/139452857-1e0248f0-5102-48b1-b43a-aed224ee9379.png)

Yes, its more safer using environment variables to store our database information, this is generally considered more secure

and besides it’s the best practice to separate configuration and secret data from the application settings

as against writing connection strings directly inside the index.js application file.I configured the MongoDb database

and the MongoDb clusters by following the screen shots as shown below

![image](https://user-images.githubusercontent.com/55473846/139453128-eca27c1b-4b63-463b-8e8e-3ffedb1dc324.png)

In the index.js file,i specified process .env to access environment variables, and latter created this file. 

I created a file in my Todo directory and name it .env.

touch .env

vi .env

I added the connection string to access the database in it, just as below:

DB=mongodb+srv://goodlord:<password>@cluster0.bp8j8.mongodb.net/DareyDb?retryWrites=true&w=majority

Now i updated the index.js to reflect the use of .env so that Node.js can connect to the database by simply deleting 
  
all existing content in the file, and update it with the entire code below.
  
I did that using vim index.js and follow below steps

I deleted the content of index.js and replaced with the content below:

const express = require('express');
const bodyParser = require('body-parser');
const mongoose = require('mongoose');
const routes = require('./routes/api');
const path = require('path');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

//connect to the database
mongoose.connect(process.env.DB, { useNewUrlParser: true, useUnifiedTopology: true })
.then(() => console.log(`Database connected successfully`))
.catch(err => console.log(err));

//since mongoose promise is depreciated, we overide it with node's promise
mongoose.Promise = global.Promise;

app.use((req, res, next) => {
res.header("Access-Control-Allow-Origin", "\*");
res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
next();
});

app.use(bodyParser.json());

app.use('/api', routes);

app.use((err, req, res, next) => {
console.log(err);
next();
});

app.listen(port, () => {
console.log(`Server running on port ${port}`)
});

When I ran node index.js
  
I got the message server running on port:5000 but no database connected successfully message immediately i knew there was a problem

  ![image](https://user-images.githubusercontent.com/55473846/139453472-ae714177-44f1-468d-8c54-3e5b73d02d97.png)
  
  I started my server using the command:
  
I had issues figuring out what was making my POST request to be failing in postman, I had to install PostmanAgent it still didn’t work.
  
http:// 13.40.3.217:5000/api/todos
  
I ran this url on postman, the public ip_address: 13.40.3.217 of my sever listening on port:5000
  
I checked the security group settings(configuration) to see if port:500 was still open it was i also checked the content
  
  of vim index.js and if the right content were properly inserted it was all ok.
  
I had to check again the content of vi .env where I stored my connection string to MongoDB 
  
  if it has been tampered with in my Todo directory, it was still ok. I latter found out it was My MongoDB database
  
  created was no longer connecting, ran a reset password and now did the configuration again to my clusters on Mongodb 
  
  site but still using the same password and username given to me initially.
  
  I now ran Node index.js and got the below response shown in the screenshots

  ![image](https://user-images.githubusercontent.com/55473846/139453737-706bd228-0cc3-49ec-a3f5-bc07447e118f.png)
  
After troubleshooting I now ran the url below on postman to test if any POST request will it work on the application proper.
  
Under headings menu in Postman
  
Key: Content-Type
  
Value: Applicationjson and
  
 under body menu: I posted this request below 
  
{

    "action": "am going home again"
}
  
As shown in the screenshots below:
  
 ![image](https://user-images.githubusercontent.com/55473846/139454012-f1bfc155-f5c1-4396-ae71-0f9cca9b09a0.png)
  
  http:// 13.40.3.217:5000/api/todos
  
After troubleshooting I equally ran the url above on postman to test if any GET request will work on the application proper, it worked and pulled out the content below and the screen shots also shows this
{
        "_id": "61729449216c194a3064dec6",
        "action": "Working on project3 right now"
    },
    {
        "_id": "6178e933908457634987617d",
        "action": "am going home again"
    }
}

  ![image](https://user-images.githubusercontent.com/55473846/139454151-cec28bdb-ef52-4c28-b481-e01f530bf98b.png)
  
I equally ran this url: http:// 13.40.3.217:5000/api/todos
  
 on the browser got this screen shots below
  
  ![image](https://user-images.githubusercontent.com/55473846/139454279-9313eb0f-eb51-4fd6-9eea-964e99c16fb5.png)
  
  Having done all these i am more than sure that I have tested the backend part of myTo-Do application and made sure that
  
  it supports all three operations needed as described below:
  
•	Show a list of tasks – HTTP GET request
  
•	Add up a new task to the list – HTTP POST request
  
•	Remove current task from the list – HTTP DELETE request
  
This shows that I have successfully created the Backend, now I have the Frontend which is the graphical user interface GUI.
  
  This is the part the clients will have access to where data is inserted (POST request) and latter submitted to the database
  
  while immediately this is done, we shall have the (GET requests) pulling out data to the interface, furthermore there would
  
  be a delete button that removes any items from the database (DELETE Requests).
  
FRONTEND CREATION
  
Step 2 – Frontend creation
  
Since we are done with the functionality we want from our backend and API, it is time to create a user interface for a Web client (browser) 
  
  to interact with the application via API. To start out with the frontend of the To-do app, we will use the create-react-app command
  
  to scaffold our app.
  
In the same root directory as your backend code, which is the Todo directory, run:

![image](https://user-images.githubusercontent.com/55473846/139454665-3da81b11-dd20-477f-9591-33ac0042046d.png)
  
  ![image](https://user-images.githubusercontent.com/55473846/139454747-09bf453e-31ed-4a67-8ee4-811c46e4162b.png)
  
  The application now opened and start running on localhost:3000
  
To be able to access the application from the Internet i must open TCP port 3000 on EC2 by adding a new Security Group rule. 
  
Creating your React Components
  
One of the advantages of react is that it makes use of components, which are reusable and also makes code modular.
  
  For our Todo app, there will be two stateful components and one stateless component.
  
From your Todo directory run

![image](https://user-images.githubusercontent.com/55473846/139455062-34865b48-9e14-4c2a-85cf-cd719246278c.png)
  
  Check the content of input.js
  
  ![image](https://user-images.githubusercontent.com/55473846/139455190-a8dd843c-b1d4-4a93-9981-d2164b5c472d.png)
  
To make use of Axios, which is a Promise based HTTP client for the browser and node.js, you need to cd into your client 
  
from your terminal and run yarn add axios or npm install axios.
  
Move to the src folder
  
cd ..

I ran npm audit
  
FRONTEND CREATION 
  
in the vi Todo.js i ran
  
npm run dev

![image](https://user-images.githubusercontent.com/55473846/139455667-17186541-aae6-41ee-b590-a954362721d3.png)
  
  import React from 'react';

import Todo from './components/Todo';
import './App.css';

const App = () => {
return (
<div className="App">
<Todo />
</div>
);
}

export default App;
 in the src directory I placed the following codes into the vi Apcss

.App {
text-align: center;
font-size: calc(10px + 2vmin);
width: 60%;
margin-left: auto;
margin-right: auto;
}

input {
height: 40px;
width: 50%;
border: none;
border-bottom: 2px #101113 solid;
background: none;
font-size: 1.5rem;
color: #787a80;
}

input:focus {
outline: none;
}

button {
width: 25%;
height: 45px;
border: none;
margin-left: 10px;
font-size: 25px;
background: #101113;
border-radius: 5px;
color: #787a80;
cursor: pointer;
}

button:focus {
outline: none;
}

ul {
list-style: none;
text-align: left;
padding: 15px;
background: #171a1f;
border-radius: 5px;
}

li {
padding: 15px;
font-size: 1.5rem;
margin-bottom: 15px;
background: #282c34;
border-radius: 5px;
overflow-wrap: break-word;
cursor: pointer;
}

@media only screen and (min-width: 300px) {
.App {
width: 80%;
}

input {
width: 100%
}

button {
width: 100%;
margin-top: 15px;
margin-left: 0;
}
}

@media only screen and (min-width: 640px) {
.App {
width: 60%;
}

input {
width: 50%;
}

button {
width: 30%;
margin-left: 10px;
margin-top: 0;
}
}
In the src directory open the index.css
vim index.css
body {
margin: 0;
padding: 0;
font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Oxygen",
"Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue",
sans-serif;
-webkit-font-smoothing: antialiased;
-moz-osx-font-smoothing: grayscale;
box-sizing: border-box;
background-color: #282c34;
color: #787a80;
}

code {
font-family: source-code-pro, Menlo, Monaco, Consolas, "Courier New",
monospace;
}
  
![image](https://user-images.githubusercontent.com/55473846/139455825-5b4acf1d-679c-40e2-a731-09f8a9daadb2.png)
  
Now on the Todo directory
  
Cd ../
  
After working in the Todo directory i ran:
  
npm run dev

![image](https://user-images.githubusercontent.com/55473846/139456092-4d433adc-98ce-4abe-9c4a-1cf257aea64d.png)
  
I made sure the Nginx server was still running, check if the Mongodb connection was still there, at this stage i ran Node.index.js
  
  again to check if the server is still running
  
Finally, since there was no errors when saving all these files, my To-Do app is now ready and fully functional
  
  with the functionality discussed earlier: creating a task, deleting a task and viewing if those task still works.
  
  I clciked the delete button it worked , send Post Request and it sent awhile I also tried the Get request and it worked .
  
  I now have have My ToDo application running
  
I ran http://<public_ip_address>:3000/
  
http://3.8.119.132:3000/
  
  
![image](https://user-images.githubusercontent.com/55473846/139456443-ae788ce7-14ea-42ab-82b6-a5012270fc45.png)
  
ln this Project i have created a simple To-Do application and deployed it to MERN stack.I wrote a frontend application using React.js 
  
that communicates with a backend application written using Expressjs. I also created a Mongodb backend for storing tasks in a database.
 





