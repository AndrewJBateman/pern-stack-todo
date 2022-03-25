# :zap: PERN Full Stack Todo

* PostgreSQL Express React Node (PERN) full-stack app, integrates React frontend with Node.js backend that is deployed to Heroku. Tutorial code by The Stoic Programmers (see 'Inspiration' below)
* **Note:** to open web links in a new window use: _ctrl+click on link_

![GitHub repo size](https://img.shields.io/github/repo-size/AndrewJBateman/pern-stack-todo?style=plastic)
![GitHub pull requests](https://img.shields.io/github/issues-pr/AndrewJBateman/pern-stack-todo?style=plastic)
![GitHub Repo stars](https://img.shields.io/github/stars/AndrewJBateman/pern-stack-todo?style=plastic)
![GitHub last commit](https://img.shields.io/github/last-commit/AndrewJBateman/pern-stack-todo?style=plastic)

## :page_facing_up: Table of contents

* [:zap: PERN Stack Todo](#zap-pern-stack-todo)
  * [:page_facing_up: Table of contents](#page_facing_up-table-of-contents)
  * [:books: General info](#books-general-info)
  * [:camera: Screenshots](#camera-screenshots)
  * [:signal_strength: Technologies](#signal_strength-technologies)
  * [:floppy_disk: Setup](#floppy_disk-setup)
  * [:wrench: Testing](#wrench-testing)
  * [:computer: Code Examples](#computer-code-examples)
  * [:cool: Features](#cool-features)
  * [:clipboard: Status & To-Do List](#clipboard-status--to-do-list)
  * [:clap: Inspiration](#clap-inspiration)
  * [:file_folder: License](#file_folder-license)
  * [:envelope: Contact](#envelope-contact)

## :books: General info

### Backend

* PostgreSQL needs to be installed and running - I started it from my Windows 10 PostgreSQL 12 dropdown option 'SQL shell (psql)'
* Postman used to test the backend before frontend was available

### Frontend

* React frontend includes a simple todo list with a user input field and a table of todos below. User can edit and delete todos
* [JavaScript XML (JSX)](https://reactjs.org/docs/introducing-jsx.html) used to write HTML elements in Javascript
* [React Fragments](https://reactjs.org/docs/fragments.html) used to show table of todos as a row with columns in the DDM

## :camera: Screenshots

![Backend screenshot](./img/postgresql.png)
![Frontend & backend screenshot](./img/todos.png)
![Frontend screenshot](./img/edit.png)

## :signal_strength: Technologies - Backend

* [PostgreSQL v12](https://www.postgresql.org/)
* [PostgreSQL Installer for Windows](https://www.postgresqltutorial.com/install-postgresql/)
* [Express.js middleware v4](https://expressjs.com/)
* [Node.js v12](https://nodejs.org/es/)
* [Nodemon](https://www.npmjs.com/package/nodemon) npm module so backend server will automatically restart after code changes
* [Postman API](https://www.postman.com/downloads/) to simulate a frontend

## :signal_strength: Technologies - Frontend

* [React framework v16](https://reactjs.org/)
* [Bootstrap v4](https://getbootstrap.com/) component library

## :floppy_disk: Dev Setup - Backend

* Install dependencies using `npm i`
* Install [nodemon](https://www.npmjs.com/package/nodemon) globally if you don't already have it
* Install [PostgreSQL](https://www.postgresql.org/) & run it (requires the password you created during installation)
* Add database access credentials to `db.js` - recommend installing [npm dotenv](https://www.npmjs.com/package/dotenv) & using .env to hide credentials if commiting to Github
* Postgresql shell commands: `\l` list all databases. `\c` database1 connect to database1. `\dt` inspect tables. `\d+` inspect table & show relation information. `\q` to quit
* From root run `nodemon server` for a dev server
* `http://localhost:5000/` can be accessed for CRUD operations such as POST, GET, PUT, DELETE etc. using Postman

## :floppy_disk: Dev Setup - Frontend

* Change to `client` directory
* Install dependencies using `npm i`.
* run `npm start`. Frontend will open at `http://localhost:3000/`

## :floppy_disk: To Deploy to Heroku

* Assumes you have [Heroku](https://www.heroku.com) installed
* Server folder contents moved to root directory. Heroku must see package.json in root
* db.js includes ternery expression to choose connection config
* package.json (server) `heroku-postbuild` script added
* Heroku scripts order: `heroku pre-build, npm install, heroku-postbuild, run start script`
* client files edited: change to use proxy for dev address
* Once package.json scripts added and you are logged into Heroku:
* Create project: `heroku create pern-stack-todoapp`
* Add Heroku database addon: `heroku addons:create heroku-postgresql:hobby-dev -a pern-stack-todoapp`
* To access Heroku database: `pg:psql -a pern-stack-todoapp`
* Run `git add .` then `git commit -m "code added for Heroku deployment"` to add all changes
* Run `heroku git:remote -a pern-stack-todoapp` - this is my example
* Run `git push heroku master` to send app to Heroku
* Run `heroku open` to open app in a browser window

## :computer: Code Examples - Backend

* backend `index.js`: express post method used to add new todo [description] to postgreSQL database using SQL INSERT INTO statement

```javascript
// create a todo
app.post('/todos', async (req, res) => {
  try {
    const { description } = req.body;
    const newTodo = await pool.query(
      "INSERT INTO todo (description) VALUES($1) RETURNING *",
      [description]
    );

    res.json(newTodo.rows[0]);
  } catch (err) {
    console.error(err.message);
  }
})
```

## :computer: Code Examples - Frontend

* function that runs when user presses 'Add' button: the input body (description) is converted from a JavaScript object to a JSON string & POSTed to the todo database

```javascript
  const onSubmitForm = async e => {
    e.preventDefault();
    try {
      const body = { description };
      const response = await fetch("http://localhost:5000/todos", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(body)
      });

      console.log("Successfully added todo: ", response);
      window.location = "/";
    } catch (err) {
      console.error(err.message);
    }
  };
```

## :cool: Features - Backend

* All data stored in PostgreSQL database that can also be viewed and changed from the PostgreSQL shell (psql)

## :cool: Features - Frontend

* React app created from the command prompt using [Create React App](https://reactjs.org/docs/create-a-new-react-app.html)
* Uses the [Bootstrap basic table](https://www.w3schools.com/bootstrap/bootstrap_tables.asp) to list todos
* [Bootstrap 4 Modal](https://www.w3schools.com/bootstrap4/bootstrap_modal.asp) dialog box

## :clipboard: Status & To-Do List

* Status: Working & deployed to Heroku.
* To-Do: Add commenting. Add npm concurrently to run front & back ends with 1 command. Add functionality. Order todos so recent one is top.

## :clap: Inspiration/General Tools

* [The Stoic Programmers, PERN Stack Course - PostgreSQL, Express, React, and Node](https://www.youtube.com/watch?v=ldYcgPKEZC8&t=116s)
* [The Stoic Programmers, How to Deploy a PERN application on Heroku](https://www.youtube.com/watch?v=ZJxUOOND5_A&t=13s)
* [React documentation](https://reactjs.org/docs/getting-started.html)
* [Enable Emmet support for JSX in Visual Studio Code | React](https://medium.com/@eshwaren/enable-emmet-support-for-jsx-in-visual-studio-code-react-f1f5dfe8809c)
* [js-beautify for VS Code](https://marketplace.visualstudio.com/items?itemName=HookyQR.beautify)

## :file_folder: License

* This project is licensed under the terms of the MIT license.

## :envelope: Contact

* Repo created by [ABateman](https://github.com/AndrewJBateman), email: gomezbateman@yahoo.com
