  :
  
 lost screenshots on github as laptop crashed.
 
  :

MONGODB DATABASE

We need a database where we will store our data. For this we will make use of mLab. mLab provides MongoDB database as a service solution (DBaaS), so to make life easy, you will need to sign up for a shared clusters free account, which is ideal for our use case. Sign up here. Follow the sign up process, select AWS as the cloud provider, and choose a region near you.

Complete a get started checklist as shown on the image below

Start your server using the command:

node index.js

![image](https://user-images.githubusercontent.com/67065306/132257908-fa9c87b4-4303-460a-a4db-25f4db1a2a36.png)

**Testing Backend Code without Frontend using RESTful API**

create a POST request to the API http://54.78.214.175:5000/api/todos

![image](https://user-images.githubusercontent.com/67065306/132495688-2edea590-36e0-47e4-b7e2-cc6815a33fdd.png)

  create a GET request to the API http://54.78.214.175:5000/api/todos
  
 ![image](https://user-images.githubusercontent.com/67065306/132495879-d2d5e4de-d475-45a0-8f06-5475e92907b8.png)

 
  Delete Request:
  
  ![image](https://user-images.githubusercontent.com/67065306/132510127-2f583b28-15df-48c0-84bf-06852b2789af.png)
  
  **STEP 2 – FRONTEND CREATION**
  
  Since we are done with the functionality we want from our backend and API, it is time to create a user interface for a Web client (browser) to 
  interact with the application via API. To start out with the frontend of the To-do app, we will use the create-react-app command to scaffold our app.

In the same root directory as your backend code, which is the Todo directory, run:

 npx create-react-app client

![image](https://user-images.githubusercontent.com/67065306/132510846-07e20840-82a5-4a74-baf7-e48f748486c0.png)

This created a new folder in our Todo directory called client, where we will add all the react code.

**Running a React App**
Before testing the react app, there are some dependencies that need to be installed.

Install concurrently. It is used to run more than one command simultaneously from the same terminal window.

npm install concurrently --save-dev

![image](https://user-images.githubusercontent.com/67065306/132511662-41a5ce3a-4631-427f-8c55-746b1f508f55.png)

Install nodemon. It is used to run and monitor the server. If there is any change in the server code, nodemon will restart it automatically and load the new changes.
npm install nodemon --save-dev

![image](https://user-images.githubusercontent.com/67065306/132511847-8527c8d4-1ea8-435d-892f-f8eca623b813.png)

In Todo folder open the package.json file. Change the highlighted part of the below screenshot and replace with the code below.

![image](https://user-images.githubusercontent.com/67065306/132512884-b412bb36-7dd2-4532-9d69-1a70aeeaa1eb.png)

**Configure Proxy in package.json**

Change directory to ‘client’

cd client

Open the package.json file

vi package.json

Add the key value pair in the package.json file "proxy": "http://localhost:5000".

The whole purpose of adding the proxy configuration in number 3 above is to make it possible to access the application directly from the browser by simply calling the server url like http://localhost:5000 rather than always including the entire path like http://localhost:5000/api/todos

![image](https://user-images.githubusercontent.com/67065306/132514335-022814cd-55a6-4865-8c42-f72575be07a2.png)


Now, ensure you are inside the Todo directory, and simply do:

npm run dev

Our app should open and start running on localhost:3000

Important note: In order to be able to access the application from the Internet we have to open TCP port 3000 on EC2 by adding a new Security Group rule. 

**Creating your React Components**
One of the advantages of react is that it makes use of components, which are reusable and also makes code modular. 
For our Todo app, there will be two stateful components and one stateless component.
From our Todo directory run

cd client
move to the src directory

cd src
Inside your src folder create another folder called components

mkdir components
Move into the components directory with

cd components

Inside ‘components’ directory create three files Input.js, ListTodo.js and Todo.js.

touch Input.js ListTodo.js Todo.js

Open Input.js file

vi Input.js
Copy and paste the following;

import React, { Component } from 'react';
import axios from 'axios';

class Input extends Component {

state = {
action: ""
}

addTodo = () => {
const task = {action: this.state.action}

    if(task.action && task.action.length > 0){
      axios.post('/api/todos', task)
        .then(res => {
          if(res.data){
            this.props.getTodos();
            this.setState({action: ""})
          }
        })
        .catch(err => console.log(err))
    }else {
      console.log('input field required')
    }

}

handleChange = (e) => {
this.setState({
action: e.target.value
})
}

render() {
let { action } = this.state;
return (
<div>
<input type="text" onChange={this.handleChange} value={action} />
<button onClick={this.addTodo}>add todo</button>
</div>
)
}
}

export default Input



To make use of Axios, which is a Promise based HTTP client for the browser and node.js, you need to cd into your client from your terminal and run yarn add axios or npm install axios.

Move to the src folder

cd ..
Move to clients folder

cd ..
Install Axios

npm install axios

![image](https://user-images.githubusercontent.com/67065306/132516647-67b5aec5-a5c4-47ee-87c5-127972d287dd.png)

**FRONTEND CREATION**

cd src/components
After that open your ListTodo.js

vi ListTodo.js

in the ListTodo.js copy and paste the following code

![image](https://user-images.githubusercontent.com/67065306/132517233-065a7525-3a8c-4075-97a2-fad7c2b851a1.png)

Then in our Todo.js file we write the following code;

![image](https://user-images.githubusercontent.com/67065306/132517629-59bed2d7-ccfa-4ea7-90c3-c00e6955e924.png)


We now need to make a little adjustment to our react code. We will Delete the logo and adjust our App.js to look like this.

Move to the src folder
cd ..
Make sure that you are in the src folder and run

vi App.js
Copy and paste the code below into it

![image](https://user-images.githubusercontent.com/67065306/132518263-20c558fa-618d-4614-8260-8a885d571865.png)


Now, in the src directory open the App.css

vi App.css
Then paste the following code into App.css:

![image](https://user-images.githubusercontent.com/67065306/132518773-9a04f9d1-bfec-4dda-bc29-ba7d13c97069.png)

In the src directory open the index.css

vim index.css

Copy and paste the code below:

![image](https://user-images.githubusercontent.com/67065306/132519176-3e7f871e-9b5e-4b34-b9af-a82edd80b9ee.png)

Go to the Todo directory

In the Todo directory we run:

npm run dev

![image](https://user-images.githubusercontent.com/67065306/132519648-21ce5f32-08a0-49f7-ba41-910f3866a57e.png)

our To-Do app should be ready and fully functional with the functionality discussed earlier: creating a task, deleting a task and viewing all your tasks.

![image](https://user-images.githubusercontent.com/67065306/132520691-d941fd45-8cab-4673-b6a6-8722995452c2.png)

In this Project #3 we have created a simple To-Do and deployed it to MERN stack. 
We wrote a frontend application using React.js that communicates with a backend application written using Expressjs. 
We also created a Mongodb backend for storing tasks in a database.


