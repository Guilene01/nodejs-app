
## The node.js example app

## Requirements

* npm
* NodeJS
* Git

Follow the steps below to to install the dependencies on ubuntu then run the application.

## Common setup
## installing  npm  and nodejs

```bash
apt install nodejs npm
```
## Install firewall

```bash
apt install ufw
```

## Clone the repo and install the dependencies.

```bash
git clone https://github.com/utrains/nodejs-test-app.git
cd nodejs-test-app
```

```bash
npm install
```
## Open port 3000
before starting the application, open port 3000 where the node app is running

```bash
ufw allow 3000
```

## To start the express server, run the following

```bash
npm run start:dev
```

Open (http://youripaddress:3000) and take a look around.
![Screenshot](Capturenode.PNG)

