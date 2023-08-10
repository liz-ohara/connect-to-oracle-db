# connect-to-oracle-db
Establishes a connection to the Oracle database and sets up sample routing for locally-hosted projects in HTML, CSS, and JS. Utilizes NodeJS. Recommended source-code editor is Visual Studio Code.

1. Clone the repository.
2. Download NodeJS and connect it to OracleDB locally.
3. Run the app.

# Clone the repository
1. On GitHub.com, navigate to the main page of the repository.
2. Above the list of files, click <> Code.
3. Copy the HTTPS URL for the repository.
4. Open Visual Studio Code.
5. Click "Clone Git Repository" and paste the copied URL.
6. Select a repository location.

If you're signing in to GitHub from Visual Studio for the first time, you may need to authorize your account by entering your username and password.

[Download Visual Studio Code - Mac, Linux, Windows](https://code.visualstudio.com/download)

# To download nodejs and connect it to OracleDB locally

# To run the project
1. Ensure the repository is cloned in Visual Studio Code and Oracle Instant Client is downloaded. Follow the sections above to do so.
2. Open the dbconfig.js file and enter your Oracle username and password
3. You may need to install the following libraries in the terminal (and any others that throw errors):
```
npm install express
npm install express-session
npm install body-parser
```
4. Make sure you are on the Villanova network, or connect to the VPN before starting the program.
5. Run "npm start" in the terminal
6. Open http://localhost:8080 and you should see the UI of your application load.
