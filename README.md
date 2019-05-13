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




