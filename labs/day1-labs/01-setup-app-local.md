# Initial Setup and Running App on Local Machine

## Work Environment

There are two environments you will be working in for the exercises today.

1. **Docker VM:** The apps and containers must be run on a Linux machine.
2. **Azure Cloud Shell:** The Azure Cloud Shell will be accessed by logging into the Azure Portal (http://portal.azure.com).

Labs 1 and 2 require the Docker VM. The subsequent labs all use the Azure Cloud Shell.

## Clone Lab Github Repo

You must clone the workshop repo to the your local machine and Docker VM.

1. Start with a terminal on the Docker VM
2. Clone the Github repo via the command line

    ```
    git clone https://github.com/kaluzaaa/azure-containers-workshop.git
    ```

## Get Applications up and running

### Database layer - MongoDB

The underlying data store for the app is [MongoDB](https://www.mongodb.com/ "MongoDB Homepage"). It is already running. We need to import the data for our application.

1. Import the data using a terminal session on the Docker VM

    ```bash
    cd ~/azure-containers-workshop/app/db

    mongoimport --host localhost:27017 --db webratings --collection heroes --file ./heroes.json --jsonArray && mongoimport --host localhost:27017 --db webratings --collection ratings --file ./ratings.json --jsonArray && mongoimport --host localhost:27017 --db webratings --collection sites --file ./sites.json --jsonArray
    ```

### API Application layer - Node.js

The API for the app is written in javascript, running on [Node.js](https://nodejs.org/en/ "Node.js Homepage") and [Express](http://expressjs.com/ "Express Homepage")

1. Update dependencies and run app via node in a terminal session on the Docker VM

    ```bash
    cd ~/azure-containers-workshop/app/api

    npm install && npm run localmachine
    ```

2. Open a new terminal session on the Docker VM and test the API

    use curl
    ```bash
    curl http://localhost:3000/api/heroes
    ```
    
### Web Application layer - Vue.js, Node.js

The web frontend for the app is written in [Vue.js](https://vuejs.org/Vue "Vue.js Homepage"), running on [Node.js](https://nodejs.org/en/ "Node.js Homepage") with [Webpack](https://webpack.js.org/ "Webpack Homepage")

1. Open a new terminal session on the Docker VM
2. Update dependencies and run app via node

    ```bash
    cd ~/azure-containers-workshop/app/web

    npm install && npm run localmachine
    ```
3. Test the web front-end

    The Docker VM has an external DNS name and port 8080 is open. You can browse your running app with a link such as: http://jump-vm-csc4f653357f-q72zm5c4ggcza.eastus.cloudapp.azure.com:8080 

    You can also test from a new terminal session in the Docker VM
    ```bash
    curl http://localhost:8080
    ```

## Clean-up

Close the web and api apps in the terminal windows by hitting `ctrl-c` in each of the corresponding terminal windows
