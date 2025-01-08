### Step 1: Set Up the Flask Application

1. **Initialize a Flask app**: Create a new directory for your project and a Python virtual environment inside it:
    
    bash
    
    Copy code
    
    `mkdir myproject cd myproject python3 -m venv venv source venv/bin/activate`
    
2. **Install Flask and create a basic app**: Create a file called `app.py` and add the following code to set up a basic Flask app:
    
    python
    
    Copy code
    
    `from flask import Flask, jsonify  app = Flask(__name__)  @app.route('/api') def hello_world():     return jsonify({"message": "Hello, World!"})  if __name__ == '__main__':     app.run(host='0.0.0.0', port=5000, debug=True)`
    
3. **Install Flask**: Make sure to install Flask in your virtual environment:
    
    bash
    
    Copy code
    
    `pip install flask`
    

### Step 2: Set Up the Next.js Application

1. **Initialize a Next.js app**: Ensure you have Node.js installed, then use `npx` to create a new Next.js app:
    
    bash
    
    Copy code
    
    `npx create-next-app frontend cd frontend`
    
2. **Modify `index.js` to call the Flask API**: Edit the `pages/index.js` file in your Next.js application to fetch data from the Flask API:
    
    javascript
    
    Copy code
    
    `import { useEffect, useState } from 'react';  export default function Home() {   const [message, setMessage] = useState('');    useEffect(() => {     fetch('http://localhost:5000/api')       .then(response => response.json())       .then(data => setMessage(data.message));   }, []);    return (     <div>       <h1>Welcome to Next.js!</h1>       <p>{message}</p>     </div>   ); }`
    
3. **Install dependencies and run the Next.js app**: Run `npm install` and `npm run dev` to start the Next.js development server. The server will be available at `http://localhost:3000`.
    

### Step 3: Create a Dockerfile

Create a Dockerfile in the root of your project directory to set up both the Flask and Next.js applications:

Dockerfile

Copy code

`# Use an official Python runtime as a parent image FROM python:3.8-slim as backend  # Set the working directory in the container WORKDIR /app  # Copy the backend application COPY ./app.py /app  # Install Flask RUN pip install flask  # Expose the port the app runs on EXPOSE 5000  # Define environment variable ENV FLASK_APP=app.py  # Run app.py when the container launches CMD ["flask", "run", "--host=0.0.0.0"]  # Use Node.js 14 as a base image for the frontend FROM node:14 as frontend  # Set the working directory for the frontend WORKDIR /app/frontend  # Copy the frontend application COPY ./frontend /app/frontend  # Install dependencies RUN npm install  # Build the Next.js app RUN npm run build  # Expose the port the Next.js server uses EXPOSE 3000  # Run the Next.js app CMD ["npm", "start"]`

### Step 4: Docker Compose

Using Docker Compose is recommended to orchestrate both the frontend and backend services. Create a `docker-compose.yml` file in the root directory:

yaml

Copy code

`version: '3.8' services:   backend:     build:       context: .       dockerfile: Dockerfile       target: backend     ports:       - "5000:5000"   frontend:     build:       context: .       dockerfile: Dockerfile       target: frontend     ports:       - "3000:3000"`

### Step 5: Run Your Application

Now, you can build and run your application using Docker Compose:

bash

Copy code

`docker-compose up --build`

This command builds both the frontend and backend images and starts the containers. Your Flask API will be accessible at `http://localhost:5000/api`, and the Next.js frontend will be accessible at `http://localhost:3000`.