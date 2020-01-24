## Enable Javascript ES6 in NodeJS using Babel

* Make a new project using ***express your-project-name --no-view*** terminal command.
* Rename ***bin/www*** to ***www.js***
* Move the ***bin/***, ***routes/*** and ***app*** into a new folder called ***src/***, and convert the code into ES6. 

#### Code for bin/www.js:
```javascript
// bin/www.js
/**
 * Module dependencies.
 */
import app from '../app'
import debugLib from 'debug'
import http from 'http'

const debug = debugLib('your-project-name:server')

/**
 * Get port from environment and store in Express.
 */
```

#### Code for routes/index.js:
```javascript
// routes/index.js
import express from 'express'
var router = express.Router()

/* GET home page. */
router.get('/', function(req, res, next) {
  res.render('index', { title: 'Express' })
})

export default router
```

#### Code for app.js:
```javascript
// app.js
import express from 'express'
import path from 'path'
import cookieParser from 'cookie-parser'
import logger from 'morgan'
import indexRouter from './routes/index'

const app = express()
app.use(logger('dev'))
app.use(express.json())
app.use(express.urlencoded({ extended: false }))
app.use(cookieParser())
app.use(express.static(path.join(__dirname, '../public')))
app.use('/', indexRouter)

export default app
```

* Install all the dependencies and devDependencies

```
npm i -D @babel/cli @babel/core @babel/node @babel/preset-env nodemon
npm i --save rimraf npm-run-all
```

* Add these scripts to your ***package.json***
```
"scripts": {
    "start": "npm run prod",
    "server": "babel-node ./src/bin/www",
    "server:prod": "node ./dist/bin/www",
    "dev": "NODE_ENV=development npm-run-all server",
    "clean": "rimraf dist",
    "build": "babel ./src --out-dir dist",
    "prod": "NODE_ENV=production npm-run-all clean build server:prod",
    "watch": "nodemon"
  },
```
* Make ***nodemon.json*** and ***.babelrc*** configuration files

#### nodemon.json:
```
{
  "exec": "npm run dev",
  "watch": ["src/*", "public/*"],
  "ext": "js, html, css, json"
}
```
#### .babelrc:
```
{
  "presets": ["@babel/preset-env"]
}
```

* Test your scripts by running ***npm run dev***, ***npm run watch*** or ***npm run prod(=npm start)***
* You’ll see the complete repo at my github

<br />
<br />
___

#### Reference: 
https://www.freecodecamp.org/news/how-to-enable-es6-and-beyond-syntax-with-node-and-express-68d3e11fe1ab/