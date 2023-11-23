# Express Web Application

A lightweight web application template for rapidly creating prototypes.

## Install dependencies

```bash
# Install node
npm init --y

# Install dependancies
npm install --save express ejs

# Install dev dependancies
npm install --save-dev nodemon
```

## Configure directories

```bash
# Create web server
touch app.js

# Create views directory
mkdir views
cd views
touch index.ejs
cd ..

# Create routes directory
mkdir routes
cd routes
touch index.routes.js
cd ..
```

## Configure scripts

```json
  "scripts": {
    "start": "node app.js",
    "dev": "nodemon app.js"
  }
```

## Basic server template

```javascript
// app.js

const express = require("express");
const routes = require("./routes/index.routes.js")

const app = express();
const port = 3000;

app.set("view engine", "ejs");

app.use(routes);

app.listen(port, () => {
  console.log("App running on http://localhost:3000");
});
```

## Basic router template

```javascript
// ./routes/routes.js

const express = require('express');
const router = express.Router();

app.get("/", (req, res) => {
  res.render("index.ejs");
});

module.exports = router;
```

## Basic view template

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Home</title>
    <link
      rel="stylesheet"
      href="https://cdn.jsdelivr.net/npm/@picocss/pico@1/css/pico.min.css"
    />
  </head>
  <body>
    <h1>Hellow World!</h1>
  </body>
</html>
```