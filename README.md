# connect-to-oracle-db
Establishes a connection to the Oracle database and sets up sample routing for locally-hosted projects in HTML, CSS, and JS. Utilizes NodeJS. Recommended source-code editor is Visual Studio Code.

1. Clone the repository.
2. Download NodeJS and connect it to OracleDB locally.
3. Run the app.

## Important notes
1. YOU CANNOT MAKE CHANGES TO THIS REPOSITORY. You may clone this repository, but you must make your own repository and then change the URL to push changes. (Steps outlined in the "Clone the repository" section.)
3. Never commit your username and password in dbconfig.js to the remote repository.
4. If you make changes to server.js, kill the terminal and re-run "npm start" to load those changes.
5. If the DB connection is not working, make sure you are on VPN or Villanova Wi-Fi.
6. Canges in Visual Studio Code are not automatically saved in the remote repository. There are a lot of resources online about working with git commands through Visual Studio Code. You can also make branches to collaborate with teammates.

## Clone the repository
1. On GitHub.com, navigate to the main page of the connect-to-oracle-db repository.
2. Above the list of files, click <> Code.
3. Copy the HTTPS URL for the repository.
4. Open Visual Studio Code.
5. Click "Clone Git Repository" and paste the copied URL.
6. Select a repository location.
7. On YOUR GitHub account, create a new repository (click on the "+" icon in the top-right corner and select "New repository"). Give it a name and configure the settings as you like.
8. Copy the HTTPS URL of your newly created repository.
9. In the Visual Studio Code terminal, with the connect-to-oracle-db project opened, run the following commands one at a time. These commands change the remote URL to your newly created repository and then pushes the code from the cloned repository to your new repository.
    
```
git remote set-url origin <url-of-new-repo>
git push origin master
```

Note: If you're signing in to GitHub from Visual Studio for the first time, you may need to authorize your account by entering your username and password.

[Download Visual Studio Code - Mac, Linux, Windows](https://code.visualstudio.com/download)

[Changing a remote repository's URL](https://docs.github.com/en/get-started/getting-started-with-git/managing-remote-repositories#changing-a-remote-repositorys-url)

## To download nodejs and connect it to OracleDB locally
Set-Up Help: https://node-oracledb.readthedocs.io/en/latest/user_guide/installation.html

Connection String Help: https://node-oracledb.readthedocs.io/en/latest/user_guide/connection_handling.html#connectionstrings

### ON MAC 
1. Install NodeJS from [nodejs.org](https://nodejs.org/en)

2. Install node-oracledb using the npm package manager, which is included in Node.js:
```
npm install oracledb
```
3. Install the free Oracle Instant Client ‘Basic’ package.
Download the Basic 64-bit DMG from [Oracle Technology Network](https://www.oracle.com/database/technologies/instant-client/winx64-64-downloads.html)

4. Install Oracle Instant Client (Scripted installation). Open the terminal and run the following commands:
```
cd $HOME/Desktop
curl -O https://download.oracle.com/otn_software/mac/instantclient/198000/instantclient-basic-macos.x64-19.8.0.0.0dbru.dmg
hdiutil mount instantclient-basic-macos.x64-19.8.0.0.0dbru.dmg
/Volumes/instantclient-basic-macos.x64-19.8.0.0.0dbru/install_ic.sh
hdiutil unmount /Volumes/instantclient-basic-macos.x64-19.8.0.0.0dbru
```

_The Instant Client directory will be $HOME/Desktop/instantclient_19_8._

_Applications may not have access to specific folders (like the Downloads directory), so pick a path to place Instant Client that is convenient._

5. Configure Instant Client

Tell node-oracledb where your Oracle Client libraries are by updating the following file path (in instantclient.js):
```
const oracledb = require('oracledb');
const fs = require('fs');
try {
  let libPath;
  if (process.platform === 'win32') {           // Windows
    libPath = 'C:\\oracle\\instantclient_19_12';
  } else if (process.platform === 'darwin') {   // macOS
    libPath = process.env.HOME + '/Desktop/instantclient_19_8';
  }
  if (libPath && fs.existsSync(libPath)) {
    oracledb.initOracleClient({ libDir: libPath });
  }
}
catch (err) {
  console.error(err);
  process.exit(1);
}
```
_If you did not place Instant Client in your Desktop folder, change the file path._

6. Edit dbconfig.js and set the database credentials to your environment, for example:
```
module.exports = {
  user          : "hr",
  password      : "pswd",
  connectString : "(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=mymachine.example.com)(PORT=1521))(CONNECT_DATA=(SERVER=DEDICATED)(SID=ORCL)))"
};
```
_For Villanova students, connectString should be:
connectString : "(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=CSDB.csc.villanova.edu)(PORT=1521))(CONNECT_DATA=(SERVER=DEDICATED)(SID=orcl)))"_

7. Run one of the examples, such as seeListings.js:
```
node seeListings.js 
```
### ON WINDOWS
1. Install NodeJS
Install the 64-bit Node.js MSI (e.g. node-v14.17.0-x64.msi) from [nodejs.org](https://nodejs.org/en).

2. Install node-oracledb using the npm package manager, which is included in Node.js:
```
npm install oracledb
```
3. Install the free Oracle Instant Client ZIP
Download the free 64-bit Instant Client Basic ZIP file from [Oracle Technology Network](https://www.oracle.com/database/technologies/instant-client/winx64-64-downloads.html)

4. Unzip the ZIP file into a directory that is accessible to your application.

For example unzip instantclient-basic-windows.x64-19.11.0.0.0dbru.zip to C:\oracle\instantclient_19_11.

5. Configure Instant Client
Tell node-oracledb where your Oracle Client libraries are by updating the following file path (in instantclient.js):
```
const oracledb = require('oracledb');
const fs = require('fs');
try {
  let libPath;
  if (process.platform === 'win32') {           // Windows
    libPath = 'C:\\oracle\\instantclient_19_12';
  } else if (process.platform === 'darwin') {   // macOS
    libPath = process.env.HOME + '/Desktop/instantclient_19_8';
  }
  if (libPath && fs.existsSync(libPath)) {
    oracledb.initOracleClient({ libDir: libPath });
  }
}
catch (err) {
  console.error(err);
  process.exit(1);
}
```
_If you did not unzip Instant Client to C:\oracle\instantclient_19_1, you need to update the directory._

6. Edit dbconfig.js and set the database credentials to your environment, for example:
```
module.exports = {
  user          : "hr",
  password      : "pswd",
  connectString : "(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=mymachine.example.com)(PORT=1521))(CONNECT_DATA=(SERVER=DEDICATED)(SID=ORCL)))"
};
```
_For Villanova students, connectString should be:
connectString : "(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=CSDB.csc.villanova.edu)(PORT=1521))(CONNECT_DATA=(SERVER=DEDICATED)(SID=orcl)))"_

7. Run one of the examples, such as seeListings.js:
```
node seeListings.js
```

## To run the project
1. Ensure the bike rental database is created in SQLDeveloper on your Villanova repository. See the "create bike db" folder for the SQL and inserts.
2. Ensure the repository is cloned in Visual Studio Code and Oracle Instant Client is downloaded. Follow the sections above to do so.
3. Open the dbconfig.js file and enter your Oracle username and password
4. You may need to install the following libraries in the terminal (and any others that throw errors):
```
npm install express

npm install body-parser
```
4. Make sure you are on the Villanova network, or connect to the VPN before starting the program.
5. Open a new terminal in Visual Studio Code and run "npm start." The console should read "Server started at http://localhost:8080" and
"Oracle connection established" if both the UI has been served locally and the Oracle connection is successfully established.
7. Open http://localhost:8080 and you should see the UI of your application load.

[Working with git in Visual Studio Code](https://code.visualstudio.com/docs/sourcecontrol/overview)

[Git Remote: Synching local changes with remote repository](https://www.atlassian.com/git/tutorials/syncing)

## Helpful Links
1. [Set Up a Simple Node Server Project](https://levelup.gitconnected.com/set-up-and-run-a-simple-node-server-project-38b403a3dc09)
2. [Download Visual Studio Code - Mac, Linux, Windows](https://code.visualstudio.com/download)
3. [Changing a remote repository's URL](https://docs.github.com/en/get-started/getting-started-with-git/managing-remote-repositories#changing-a-remote-repositorys-url)
4. [Using Git source control in VS Code](https://code.visualstudio.com/docs/sourcecontrol/overview)
