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

Creating your React Components
One of the advantages of react is that it makes use of components, which are reusable and also makes code modular. 
For our Todo app, there will be two stateful components and one stateless component.
From your Todo directory run

cd client
move to the src directory

cd src
Inside your src folder create another folder called components

mkdir components
Move into the components directory with

cd components
