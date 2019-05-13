# MERN-STACK-Checklist

1. Create Directory 
2. Git Init 
3. Git remote add origin “link” from new git repository 
4. Touch Readme.md 
5. Git Add/Commit -m/ Push Origin Master
6. Npm init 
7. Npm i express mongoose concurrently dotenv nodemon 
8. Mkdir db routes controllers models 
9. Touch server.js .gitignore .env 
10. Cd into db/ touch connection.js seeds.js 
11. Cd into routes/ touch index.js
12. Cd into models/ touch necessary models 
13. Code . 
14. Add node_modules and .env to git ignore 
15. Add code below to server.js: 

### Express Server.js
const express = require('express')
const app = express()
const routes = require('./routes/index')

app.use(express.urlencoded({
    extended: true
}))

app.use(express.json())

app.use(express.static(__dirname + '/client/build/'))

app.get('/', (req, res) => {
    res.sendFile(__dirname + '/client/build/index.html')
})

app.use('/', routes)

const PORT = process.env.PORT || 3001

app.listen(PORT, () => {
    console.log(`Server is listening on PORT: ${PORT}`)
})

---
6. Add code below to db/connection.js: 


require('dotenv').config();
const mongoose = require("mongoose")

mongoose.connect(process.env.MONGODB_URI, { useNewUrlParser: true }).then(() => {

    console.log("MONGODB is now connected")
})


module.exports = mongoose;

---

17. Add db name to .env file (view below) 


MONGODB_URI=mongodb://localhost/dbnamehere

---
18. Changes to package.json

  "scripts": {
    "start": "node server.js",
    "dev": "concurrently \"nodemon server.js\" \"cd ./client && npm start \" ",
    "test": "echo \"Error: no test specified\" && exit 1",
    "postinstall": "cd client && npm install && npm run build"
  }

Add to the End

 "engines": {
    "node": "10.13.0"
  }

  ---
### Model Example

  const mongoose = require('../db/connections')

const Schema = mongoose.Schema

const User = new Schema({

    username: String,

    password: String,

    ideas: [

        { type: Schema.Types.ObjectId,
	ref: 'Idea' }
	]

})

module.exports = mongoose.model('User', User)

## Seeds Example

const User = require('../models/User')

const Idea = require('../models/Idea')

const mongoose = require('./connections')

const mars = new Idea({

    title: 'Fly to Mars',

    description: "Earth isn't Red enough. Let's move to a new planet"

})

const tesla = new Idea({

    title: 'Build a Car',

    description: "Gas is too expensive. I'm gonna build a car that doesn't need gas"

})



const elon = new User({

    username: 'elon_musk',

    password: 'spaceiscool',

    ideas: [mars, tesla]

})


User.remove({})

    .then(() => Idea.remove({}))

    .then(() => Idea.insertMany([mars, tesla]))

    .then(() => elon.save())

    .then(() => console.log('Successful Save'))

    .then(() => mongoose.connection.close())

## Client/React App

1. Inside express server dir => create-react-app client
2. Cd into client 
3. Npm I styled-components axios react-router-dom 
4. Cd src => Mkdir components 
5. Cd components => touch necessary components 
6. Add proxy to Package.json (after “private:true”) => "proxy": "http://localhost:3001",





