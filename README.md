# connect-to-oracle-db
Establishes a connection to the Oracle database and sets up sample routing for locally-hosted projects in HTML, CSS, and JS. Utilizes NodeJS. Recommended source-code editor is Visual Studio Code.

1. Clone the repository.
2. Download NodeJS and connect it to OracleDB locally.
3. Run the app.

## Clone the repository
1. On GitHub.com, navigate to the main page of the repository.
2. Above the list of files, click <> Code.
3. Copy the HTTPS URL for the repository.
4. Open Visual Studio Code.
5. Click "Clone Git Repository" and paste the copied URL.
6. Select a repository location.

If you're signing in to GitHub from Visual Studio for the first time, you may need to authorize your account by entering your username and password.

[Download Visual Studio Code - Mac, Linux, Windows](https://code.visualstudio.com/download)

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
cd $HOME/Downloads
curl -O https://download.oracle.com/otn_software/mac/instantclient/198000/instantclient-basic-macos.x64-19.8.0.0.0dbru.dmg
hdiutil mount instantclient-basic-macos.x64-19.8.0.0.0dbru.dmg
/Volumes/instantclient-basic-macos.x64-19.8.0.0.0dbru/install_ic.sh
hdiutil unmount /Volumes/instantclient-basic-macos.x64-19.8.0.0.0dbru
```

_The Instant Client directory will be $HOME/Downloads/instantclient_19_8._

_Applications may not have access to the Downloads directory, so you should move Instant Client somewhere convenient._

5. Configure Instant Client
Tell node-oracledb where your Oracle Client libraries are by updating the following file path (in index.js):
```
const oracledb = require('oracledb');
try {
  oracledb.initOracleClient({libDir: **'/Users/your_username/Downloads/instantclient_19_8'**});
} catch (err) {
  console.error('Whoops!');
  console.error(err);
  process.exit(1);
}
```
_If you did not place Instant Client in your Downloads folder, change the file path._

6. Edit dbconfig.js and set the database credentials to your environment, for example:
```
module.exports = {
  user          : "hr",
  password      : "pswd",
  connectString : "(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=mymachine.example.com)(PORT=1521))(CONNECT_DATA=(SERVER=DEDICATED)(SID=ORCL)))"
};
```
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
Tell node-oracledb where your Oracle Client libraries are by updating the following file path (in index.js):
```
const oracledb = require('oracledb');
try {
  oracledb.initOracleClient({libDir: **'/Users/your_username/Downloads/instantclient_19_8'**});
} catch (err) {
  console.error('Whoops!');
  console.error(err);
  process.exit(1);
}
```
_If you did not place Instant Client in your Downloads folder, change the file path._

6. Edit dbconfig.js and set the database credentials to your environment, for example:
```
module.exports = {
  user          : "hr",
  password      : "pswd",
  connectString : "(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=mymachine.example.com)(PORT=1521))(CONNECT_DATA=(SERVER=DEDICATED)(SID=ORCL)))"
};
```
7. Run one of the examples, such as seeListings.js:
```
node seeListings.js
```

## To run the project
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

## Set Up a Simple Node Server Project
https://levelup.gitconnected.com/set-up-and-run-a-simple-node-server-project-38b403a3dc09
