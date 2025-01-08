### Step 1: Install Prerequisites

Make sure you have the following installed:

- [.NET SDK](https://dotnet.microsoft.com/en-us/download)
- Node.js and npm
- [Visual Studio Code](https://code.visualstudio.com/) or any other preferred IDE

### Step 2: Create a New .NET Web API Project

Open a terminal or command prompt and run the following command to create a new .NET Web API project:
`dotnet new webapi -n MyDotnetNextApp`

This will create a new folder named `MyDotnetNextApp` with a .NET Web API project.

### Step 3: Navigate to the Project Directory

Change to the project directory:

`cd MyDotnetNextApp`

### Step 4: Add Next.js App

Use the `npx` command to create a new Next.js app inside your .NET project:

`npx create-next-app@latest client-app`

This will create a new Next.js app in the `client-app` directory within your .NET project.

### Step 5: Install Axios in the Next.js App

Navigate to the `client-app` directory and install Axios:

`cd client-app npm install axios`

### Step 6: Create a Sample API Endpoint in .NET

In your .NET project, open the `Controllers/WeatherForecastController.cs` file and add a new endpoint:

`[HttpGet("sample")] public ActionResult<string> GetSample() {     return "Hello from .NET API!"; }`

### Step 7: Call the API from Next.js using Axios

In your Next.js app (`client-app`), open the `pages/index.js` file and modify it to call the .NET API using Axios:

`import axios from 'axios'; import { useEffect, useState } from 'react';  export default function Home() {   const [message, setMessage] = useState('');    useEffect(() => {     axios.get('http://localhost:5000/WeatherForecast/sample')       .then(response => setMessage(response.data))       .catch(error => console.error(error));   }, []);    return (     <div>       <h1>Next.js Front-End</h1>       <p>Message from .NET API: {message}</p>     </div>   ); }`

### Step 8: Run the .NET API

In the terminal, make sure you are in the root directory of your .NET project (e.g., `MyDotnetNextApp`) and run:

`dotnet run`

This will start the .NET Web API server.

### Step 9: Run the Next.js App

Open a new terminal window, navigate to the `client-app` directory, and run:

`npm run dev`

This will start the Next.js development server and open the app in your default web browser.

### Step 10: Test the Application

You should now have both the .NET API and the Next.js app running. You can test the API by accessing `http://localhost:5000/WeatherForecast/sample` and the Next.js app at `http://localhost:3000`. The Next.js app should display the message "Hello from .NET API!" fetched from the .NET API.