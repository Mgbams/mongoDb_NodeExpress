# MONGODB USAGE

## INSTALLING MONGODB SHELL LOCALLY IN LINUX-UBUNTU

To get instructions or steps for installing MongoDb on your ubuntu, Visist this link

[MongoDB Documentation]('https://docs.mongodb.com/manual/tutorial/insert-documents/')
Then follow the below steps
To work locally on your home directory. Below, your_home_directory_name is your directory name. You can type the below
code in your Terminal.

```
cd  /home/your_home_directory_name
```

Once in your home directory, follow the instructions on the MongoDB Documentation. Below are the codes to add

```
wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | sudo apt-key add -
```

The operation should respond with an OK.

However, if you receive an error indicating that gnupg is not installed, you can:

#### Install gnupg and its required libraries using the following command:

```
sudo apt-get install gnupg
```

#### Once installed, retry importing the key:

```
wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | sudo apt-key add -
```

## Create a list file for MongoDB
 Change to the following directory from your terminal

```
    cd /etc/apt/sources.list.d
    touch mongodb-org-4.2.list
```
To know the version of your ubuntu, you can enter the following command on the terminal

```
lsb_release -dc
```
Then add contents to the file created using the command below:

```
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.2.list
```
[JSON Formatter]('https://jsonformatter.curiousconcept.com')
Copy your json code and paste it in the space provided for code validation in the site above. 
In the option of JSON Template, select **Compact**.
Then tick the box **Fix JSON**.
In JSON specification, select **RFC 8259**.

## Reload local package database.

Issue the following command to reload the local package database:
```
sudo apt-get update
```

## Install the MongoDB packages.

You can install either the latest stable version of MongoDB or a specific version of MongoDB.
```
sudo apt-get install -y mongodb-org
```

After the installation, You can start the mongod process by issuing the following command:
```
sudo systemctl start mongod
```

If you receive an error similar to the following when starting mongod:
Failed to start mongod.service: Unit mongod.service not found.

Run the following command first:
```
sudo systemctl daemon-reload
```
Then run the start command below again.
```
sudo systemctl start mongod
```
Verify that MongoDB has started successfully
```
sudo systemctl status mongod
```
##  To Stop MongoDB.
You can restart the mongod process by issuing the following command:
```
sudo systemctl stop mongod
```
## To Restart MongoDB
You can restart the mongod process by issuing the following command:
```
sudo systemctl restart mongod
```
## Working with MongoDB Atlas
Open a MongoDB Atlas account online and in the tabs opened in MongoDB Atlas,

* Click on *Clusters*
* Under SANDBOX, click on *connect*
* Click the last option that says *Connect with mongoDB Compass*
* Click on *I have a Compass*
* Copy the connection string at no 2, and open MongoDB Compass:
* Open your MongoDB Compass and click on **FAVORITE** next to **New Connection**.
* Add a name in the name field and choose a colour. Then click on te **SAVE** Button.
* In the *Paste your connection string (SRV or Standard )* box, paste the connection string you copied from your MongoDB Atlas.
    ```
        mongodb+srv://kingsley:<password>@cluster0-bxzn7.mongodb.net/test
    ```
* In the string you pasted, In the space reserved in it for **password** copy and paste the auto-generated password you got from
  your mongoDB Atlas. e.g, my MongoDB password is *bJhVTRKDJlSVy33C* i will have a link that looks like below after replacing
  my password into the copied string.
  ```
  mongodb+srv://kingsley:bJhVTRKDJlSVy33C@cluster0-bxzn7.mongodb.net/test
  ```

* Click **Connect**

# CREATING AN APPLICATION FOR CONNECTING TO MONGODB
Steps to follow:
* First, enter in administrative mode in ubuntu using the below command
```
sudo -S
```
* Type the below command to install express-generator
 ```
 npm install -g express-generator
 ```

 * Then return to your home directory by typing the below command:
 ```
 ctrl + D
 ```
 * While in your home directory, create a directory and give it a name as follows:
 ```
 $ mkdir test
 $ cd test
 $ express projectName --pug
 $ cd projectName
 $ npm install
 npm start
 ```
__Note:__ On the navigator, after you have typed in npm start on your terminal, type this below in the
navigator to open up your server
```
localhost:3000
```


# ROUTING USING Pug IN MongoDB

The steps are as follows:

* Right-click on your project folder and create a folder e.g api
* Inside your api folder, create a file e.g apirequest
* Open your index.js file and copy the contents and then paste the contents in your newly created **apirequest** file.

The contents copied will be of the below formats: 

```
var express = require('express');
var router = express.Router();

/* GET home page. */
router.get('/', function(req, res, next) {
  res.render('index', { title: 'Express' });
});

module.exports = router;

```
* Now modify the contents copied into your apirequest file as follows:

```
var express = require('express');
var router = express.Router();

/* GET home page. */
router.get('/apirequest', function(req, res, next) {
    console.log("hello worlds of shame");
    res.send('Ok for the moment');
  });

module.exports = router;
```
**NOTE:** The changes made into the apirequest files are the following:
1. We added the route location of our apirequest file as shown here
```
router.get('/apirequest', function(req, res, next)
```
We added our filename, called apirequest after the / symbol.

2. Then we removed the render method and replaced it with send. and inside the send method we added our output.
That is shown below:
```
res.send('Ok for the moment');
```
## Adding sub-routes to our created apirequest file and creatin a json file in the new route to be displayed on the screen

Open your apirequest file and add the following route under the firstly created route drection

```
 router.get('/apirequest/json', function(req, res, next) {
    const apijson = {
        name: "kingsley",
        surname: "mgbams",
        school: "m2i"
    }
    res.send(apijson);
  });
```
**EXPLANATION:** We added a sub-route called json to our apirequest route and we have the following route:
```
router.get('/apirequest/json', function(req, res, next)
```
It means in the route direction /apirequest, we have a sub-route called json.


## Updating our created file in the app.js file so it is aware of the newly created file apirequest
Open your  app.js file and then do the folowing:

* Add the route direction you created in your apirequest file inside the app.js file. Add it under the 
following code: 
```
var usersRouter = require('./routes/users');
```
Type the below code under the code above to add it:
```
var apirequest = require('./api/apirequest');
```
**NOTE:** We declare a variable called **apirequest** and then we target the direction of our created file. In this
case, we add it inside the **require** method. That is require('./api/apirequest')

3. We then add the codes under the following code:
```
app.use('/users', usersRouter);
```
Under the code above add this below code: 

```
app.use('/api', apirequest);
```
**NOTE:** The first parameter(/api) in the code above is the folder where your file is located.
WHILE the second parameter(apirequest) is the name of the **variable** where you saved the location to your api.

You can then start your server by typing:

```
npm start
```
Then open your browser and type
```
localhost:3000/api/apirequest
```
This opens your project in the route location specified.
**NOTE:** The problem with using npm start in Pug is that it does not offer hot-reload. Meaning at each 
modification you do in your code, you have to stop and relance the server to register the changes. That is, you
have to press the below keys to relance the server:
```
$ Ctrl + C 
$ npm start
```
-- Ctrl + C will stop the server
-- npm start will start the server.

But to be able to use a hot-reload, We can install nodemon in our project folder as follows:
In your open project, open a terminal and in the prompt, enter the below command:
```
npm i nodemon --save-dev
```
The above command will install a nodemon dependency in your package.json file and also will be installed
directly into your __node_modules/bin__ folder. You can click on refresh on Vscode if you don't see
nodemon in your __node_modules/bin__ folder. Sometimes it needs a refresh to be able to display.
Then open your package.json file and add the below script under the scripts tab.

```scripts
 "start:dev":"node_modules/.bin/nodemon ./bin/www"
```
Save the modification registered. The code above can be explained as:

*  "start:dev": This is the name we use to represent the command when we type it in the terminal
* "node_modules/.bin/nodemon" :- This is the location of the nodemon installed in our bin folder
* ./bin/www :- This is the location of the file we want to open with our  installed nodemon.

Then open your terminal and type:
```
npm run start:dev
```
This above command will open your project in hot-reload mode, meaning you don't have to reload your page to register 
changes.

# CONNECTING MY APPLICATION TO MONGODB DATABASE TABLE

* Create a folder called **config** at the root of your application folder
* Inside the **config** folder, create a file called *database.js*
* Open MongoDB Atlas at mongodb.com
* Click on clusters
* click on connect
* Select connect your application
* copy the url given e.g mongodb+srv://kingsley:<password>@cluster0-bxzn7.mongodb.net/test?retryWrites=true&w=majority
* Then in your *database.js* file create a **module.exports** object and add your link into it as shown below:

  ```
    module.exports = {
      database: process.env.MONGO_URL || 'mongodb+srv://kingsley:bJhVTRKDJlSVy33C@cluster0-bxzn7.mongodb.net/sample_training?retryWrites=true&w=majority',
      secret: 'mysecret',
    }
  ```
From the above, replace the <password> with the password generated from MongoDB Atlas.
You will have something like this below:
```
mongodb+srv://kingsley:bJhVTRKDJlSVy33C@cluster0-bxzn7.mongodb.net/test?retryWrites=true&w=majority
```
Then replace the word *test* in the link to the database you want to connect to e.g **sample_training**

## INSTALLING MONGOOSE

> Use the below command to install mongoose:

```
npm install --save mongoose
```
Then do the following things:
* Open the file that has your routage e.g in this case, open apirequest.js or menus.js
* Add the following declaration to add the mongoose you just installed

```
  const mongoose = require('mongoose');
```
Make sure you add the above code before
```
var router = express.Router();
```
* create a folder called **model** at the root of our application.
In the model folder, create a file with the same name as the name of the database located in MongoDB Compass
which contains the collection we want to display e.g sample_training.js

* In sample_training.js, Import the the installed mongoose as shown below
```
var mongoose = require('mongoose');
```
* Then create the structure of the model you want to get from the database. Here, i want to get contents
from the **companies** collection located in sample_training.
I will look at the contents of the companies collection to know its contents and i will decide on what i want
to display on my model and fill it out accordingly as follows:

```
// Schema Companies

const companiesSchema = mongoose.Schema({

    name: {
        type: String,
        required: false
    } 

});
const Companie = module.exports = mongoose.model('Companie', companiesSchema);
```

**Note:** If the collection is not in plural, that is it does not have an **s** at the end of its name e.g data, 
then you have to add a third argument in the **mongoose.model** method as follows:

```
// Schema data

const dataSchema = mongoose.Schema({

    name: {
        type: String,
        required: false
    } 

});
const Data = module.exports = mongoose.model('Data', companiesSchema, 'data');
```
From the above code, note that i added the name of the collection *data* as a third argument.
This is to force pug to search for the collection called *data* because by default it searches for
collections with *s* at the end and when we don't have an *s* at the end of our collection then we
have to force the search by adding it as a third argument.

**Explanation of the code above:** 
- Declare a schema for the collection. My collection name is companies in small letters. so i will have
```
const companiesSchema
```

- Equate it to mongoose.Schema and declare its key as an object with **type** and required

* Import the model you created and save it in a const with a name that starts in **capital letter** e.g
//IMPORTER DES MODELS
```
const Sample = require('../model/sample_training');
```
**NOTE:** Make sure you get the directions right for the model.

* Create a router that will display the contents of your model in a a page you specicy in the route
e.g 
```
router.get('/list', (req, res, next) => {
   Sample.find({}).exec((err, companies) => {
      if(err) {
        res.send(err);
      } else {
        console.log(companies);
        res.send(companies);
      }
    })
  });
  ```
**Explanation:** We specify the route location as /list and then we use the find() method on the const Sample, 
note that Sample is the variable that stores the instance of our database collection i.e it is the variable that
stores our model.

## PROJECT STRUCTURE FOR PUG

```
|_ api
  |_apirequest.js
  |_movies.js
  |_menus.js
|_ bin
   |_ www
|_ config
   |_database.js
|_ package.json
|_ app.js
|_ model
   |_sample_training.js
   |_movies.js
   |_menus.js
|_public
  |_images
  |_stylesheet
  |_javascripts
|_routes
|_views
|_node_modules
```
*In Pug, a file in .pug is like our .html file and a file in .js is like our .ts file in angular*

**NOTE:**
```
 Sample.find({ property_type: { $eq: "House"} }, { name: 1, summary: 1}).exec((err, listingsAndReviews) => {
      if(err) {
        res.send(err);
      } else {
        console.log(listingsAndReviews);
        res.send(listingsAndReviews);
      }
    })
```
From the query above, we have { name: 1, summary: 1} which means that we are interested in showing results with *name* and *summary* fields

## INSTALLING POSTMAN IN UBUNTU

> Type the following command
```
sudo snap install postman
```  
## HOW TO USE POSTMAN 

 * Open PostMan
 * Click on New
 * Select Request
 * Add a Request name
 * Add a Request description (Optional)
 * Select a collection or folder to save to and then click save
 * In the query tab of postman, add your website link for the query and select a method 

 NOTE: We have different methods like GET, POST, DELETE, PUT

## UNDERSTANDING ROUTAGE IN PUG 
> The general syntax of router.get is:
 router.get('myroute', auth(), check(isemail, isempty), (req, res, next) => {})

 NOTE: The second and third parameter is always optional.

router.get('/list', (req, res, next) => { } )

- The first parameter of router.get is the route direction. that is the link that shows on the address bar on navigation. e.g **/list**
- The second argument of router.get **(req, res, next)** are explained below
  * req is used along with post method to send data to the server. It means request and can  be used as shown below to get data
  * res is used along with get method to receive data from the server.
   ```
   req.body.title
   ```
   If we have a model called **Movie**, we can create an instance of it as follows:
   ```
   cost myMovie = new Movie();
   myMovie.title = req.body.title
   myMovie.save()
   ```
   myMovie.save() is used to save all the the changes made to myMovie.

   # Organising folders, controllers and models for routing

   * Create a folder called **api**
   * Inside the folder api, create a route file to your model. e.g for a movie route, create a file called movie.js inside api.
    Then inside movie.js, we have:
    Note that we have our database query inside the router.get() method.
    ```
    var express = require('express'); // import this file as it is necessary
    var router = express.Router();    // import this file as it is necessary

    const Movies = require('../model/movies'); // This is the direction of your movie model

    router.get('/movies', (req, res, next) => {

    const movies = Movies.aggregate([
  
      { "$group": { "_id": { "year": "$year" }, "Total": { "$sum": 1 } } },
  
      { "$project": { "year": "$_id.year", "Total": "$Total", "_id": 0 } },
  
      { "$sort": { "year": 1 } }
  
    ])
    .exec((err, mMovies) => {
  
      if (err) {
        res.send(err);
      } else {
        console.log(mMovies);
        res.send(mMovies);
      }
  
    });
  
  });

  module.exports = router;  // Import this file as it is necessary

  ```
  
* Create a folder called **model** and inside your folder model, create a file called movies.js which is your movies model.
  Then in your model, create your model as shown: 

```
var mongoose = require('mongoose');

// Schema moviesSchema

const moviesSchema = mongoose.Schema({

    title: {
        type: String,
        required: false
    }, 
    poster: {
        type: String,
        required: false
    }
});
const Movie = module.exports = mongoose.model('Movie', moviesSchema);

```

  # STEPS
  1. create a file called movies.js in the api directory
  2. Create a variable in app.js that points to the movies.js
  3. Create the route access tp movies.js with app.use in app.js
  4. In movies.js, import
   a. express
   b. router
   c. the ligne exports = router
   Note: Option c must appear at the end of the line


   # HOW TO CONNECT YOUR ANGULAR APPLICATION TO YOUR MONGODB DATABASE
   > The below steps should be followed

   * Open your angular project and create your components with the command below e.g movies component

   ```
   npm run ng generate component movies
   ``` 
   * Open src/environments/environment.ts file and add the principal link of your database e.g
   Here i created a variable apiUrl inside the environment class that points to the location of my mongoDB website

   ```
   export const environment = {
      apiUrl: 'http://localhost:3000/'
    };
   ```

   * Create a service in your angular application using the command below e.g request service

   ```
   npm run ng generate service result
   ```

* In result service, import the environment class as follows e.g
   ```
   import { environment } from '../../environments/environment';
   ```
   Then create a variable in your service and assign it the variable you created in environment e.g

   ```
    public mApiUrl = environment.apiUrl;
   ```
   * This is the most important step to link to the specific page of your database. if you are making a request to the list page
   of the backend. we can do this request for example in a http function as follows:
   ```
    getMoviesList(): Observable<Movie[]> {
      const url = `${this.mApiUrl}movies/list`;
      return this.http.get<Movie[]>(url);
  }
   ```
   **EXPLANATION:** I declared a const url and assigned it my mApiUrl. but i added the complete route to the query am targeting from
      my database. I added movies/list to it. Here, the link 
      **movies** is declared inside app.js as a link to the **movies** file. Here is its declaration in my database
      The **movies** file is the file contained in api folder and not the one contained in model.

      ```
      var moviesRouter = require('./api/movies');
      app.use('/movies', moviesRouter);
      ```
      Inside the router code below, we have a variable **Movie** which points to Movie file we declared in our model.
      We add the link to the movie file as follows:
    
      ```
      const Movies = require('../model/movies');
      ```
      And in **movies** file i made a route with the direction **/list** which contains my database query.
      In the **movies** file we have a route pointing to **/list** as follows e.g

      ``
    router.get('/list', (req, res, next) => {

        Movies.find({}).limit(50).exec((err, mMovies) => {

        if (err) {
          res.send(err);
        } else {
          console.log(mMovies);
          res.send(mMovies);
        }

      });

    });

    ```
    
__IN CONCLUSION:__ You have to target the query in your databse that will give you your results.

* Now, in your your angular app you can resolve the promise in the result service for displaying it in your template.

* IN your Movies file you create a routage to your CRUD operations that will query your databe. You must add these three necessary links 

  ```
  var express = require('express');
  var router = express.Router();

  ----------------------------------
           Code Here
  ----------------------------------
  module.exports = router;
  ```

Example: 

```
var express = require('express');
var router = express.Router();

const Movies = require('../model/movies');


// **READ** OPERATION:  THere is exec() method in FIND but no catch

router.get('/list', (req, res, next) => {

  Movies.find({}).limit(50).exec((err, mMovies) => {

      if (err) {
        res.send(err);
      } else {
        console.log(mMovies);
        res.send(mMovies);
      }

    });

});

// **READ** OPERATIONOF CRUD USING PATTERN: Example with regex search has exec() but no try

router.get('/seekwithpattern/:pattern', async (req, res, next) => {
  console.log('pattern : ', req.params.pattern);
  //const mId = req.params.id;
  //console.log(mId);
  const pattern = req.params.pattern;
  Movies.find({ title: new RegExp(pattern) })
    .exec((err, mMovies) => {

      if (err) {
        res.send(err);
      } else {
        console.log(mMovies);
        res.send(mMovies);
      }

    });

});

// **READ** OPERATION BY ID OF CRUD: SEARCHING BY ID, Here we don't use a try and catch function and you must select GET as a method
router.get('/:id', async (req, res, next) => {

  //const mId = req.params.id;
  //console.log(mId);

  Movies.findById(req.params.id).exec((err, mMovies) => {

    if (err) {
      res.send(err);
    } else {
      console.log(mMovies);
      res.send(mMovies);
    }

  });

});


// **CREATE** OPERATION OF CRUD: To Create a new record or inputs. We also use a TRY catch here.

router.post('/new', async (req, res, next) => {

  const nMovies = new Movies();
  nMovies.title = req.body.title;

  try {
    await nMovies.save();
    res.send(nMovies);
  } catch (err) {
    res.status(400).send(err);
  }
});

// **UPDATE** OPERATION OF CRUD:  TO UPDATE DATA IN MY DATABASE WITH TRY

router.put('/update/:id', async (req, res, next) => {

  // console.log(req.params.id);
  let updatedMovie = (({ title, plot, rated }) => ({
    title, plot, rated
  }))(req.body);

  try {
    const movie = await Movies.findByIdAndUpdate(req.params.id, updatedMovie, { new: true });
    res.send(movie);
  } catch (err) {
    res.status(400).send(err);
  }
});

// **DELETE** OPERATION OF CRUD:  DELETE A FILM BY ID

router.delete("/delete/:id", async(req, res, next) => {
  await Movies.deleteOne({ _id: req.params.id }, (err) => {
    if (err) {
      console.log(err);
    } else {
      res.send();
    }
  });
});


// Only POST and PUT uses try and catch but they don't use EXECUTE. 

module.exports = router;

```


