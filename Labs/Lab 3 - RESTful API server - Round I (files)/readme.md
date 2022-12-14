# Lab 3 - RESTful API Server - Round I (Files)
## Goals: 
- To build a basic RESTful API server.
- Test using POSTMAN/Thunder Client
- To Deploy server on Heroku  
## Keywords:
- Node.JS
  - `fs` module
    - `writeFile()`
    - `readFile()`
  - Async Programming 
    - Promises   
    - Async/Await
    - `util.promisify()`
- Express.JS
  - `app.get()` 
    - `req.params` object
  - `app.post()` 
    - `req.body`
  - `app.put()` 
  - `app.patch()` 
  - `app.delete()` 
  - `app.use(express.json())` method to add a middleware
  - `app.listen()` 
- JS
  - `map()` and `filter()` functions
  - JS *objects* and *arrays*


Table of Contents
=================

* [Lab 3 - RESTful API Server - Round I (Files)](#lab-3---restful-api-server---round-i-files)
   * [Goals:](#goals)
   * [Keywords:](#keywords)
* [Table of Contents](#table-of-contents)
   * [Next lab: RESTful API Server - Round II](#next-lab-restful-api-server---round-ii)
   * [Steps](#steps)
      * [Create a Package](#create-a-package)
      * [Add the data as JS object](#add-the-data-as-js-object)
      * [Run the server](#run-the-server)
      * [Test the server using Thunder Client Extension](#test-the-server-using-thunder-client-extension)
      * [Work on the Express.JS routes](#work-on-the-expressjs-routes)
   * [Challenge -  How to read/write the unicorns to a file](#challenge----how-to-readwrite-the-unicorns-to-a-file)
* [Deploy your site to Heroku](#deploy-your-site-to-heroku)
* [Challenges](#challenges)
* [Food for thought <g-emoji class="g-emoji" alias="apple" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/1f34e.png">🍎</g-emoji>](#food-for-thought-)

 
---
## Next lab: RESTful API Server - Round II
We will be using a database instead of a reading/writing to a file.

---
## Steps
### Create a Package
- Create a Node.JS package and install express.js
- Add the following routes stubs to your file:

```js
// app.get('/api/v1/unicorns')           // - get all the unicorns
// app.post('/api/v1/unicorn')          // - create a new unicorn
// app.get('/api/v1/unicorn/:id')       // - get a unicorn
// app.patch('/api/v1/unicorn/:id')     // - update a unicorn
// app.delete('/api/v1/unicorn/:id')       // - delete unicorn
```

---
### Add the data as JS object 
- create a new file *data.js* with the following content:

```js
exports.unicornsJSON  = [
  {
    "_id": "6324fbe4998cf52fe226fb96",
    "name": "Horny",
    "dob": "1992-03-13T15:47:00.000Z",
    "loves": [
      "carrot",
      "papaya"
    ],
    "weight": 600,
    "gender": "m",
    "vampires": 63
  },
  {
    "_id": "6324fbe4998cf52fe226fb97",
    "name": "Aurora",
    "dob": "1991-01-24T21:00:00.000Z",
    "loves": [
      "carrot",
      "grape"
    ],
    "weight": 450,
    "gender": "f",
    "vampires": 43
  },
  {
    "_id": "6324fbe4998cf52fe226fb98",
    "name": "Unicrom",
    "dob": "1973-02-10T06:10:00.000Z",
    "loves": [
      "energon",
      "redbull"
    ],
    "weight": 984,
    "gender": "m",
    "vampires": 182
  },
  {
    "_id": "6324fbe4998cf52fe226fb99",
    "name": "Roooooodles",
    "dob": "1979-08-19T01:44:00.000Z",
    "loves": [
      "apple"
    ],
    "weight": 591,
    "gender": "m",
    "vampires": 99
  },
  {
    "_id": "6324fbe4998cf52fe226fb9a",
    "name": "Solnara",
    "dob": "1985-07-04T09:01:00.000Z",
    "loves": [
      "apple",
      "carrot",
      "chocolate"
    ],
    "weight": 550,
    "gender": "f",
    "vampires": 80
  },
  {
    "_id": "6324fbe4998cf52fe226fb9b",
    "name": "Ayna",
    "dob": "1998-03-07T16:30:00.000Z",
    "loves": [
      "strawberry",
      "lemon"
    ],
    "weight": 733,
    "gender": "f",
    "vampires": 40
  },
  {
    "_id": "6324fbe4998cf52fe226fb9c",
    "name": "Kenny",
    "dob": "1997-07-01T17:42:00.000Z",
    "loves": [
      "grape",
      "lemon"
    ],
    "weight": 690,
    "gender": "m",
    "vampires": 39
  },
  {
    "_id": "6324fbe4998cf52fe226fb9d",
    "name": "Raleigh",
    "dob": "2005-05-03T07:57:00.000Z",
    "loves": [
      "apple",
      "sugar"
    ],
    "weight": 421,
    "gender": "m",
    "vampires": 2
  },
  {
    "_id": "6324fbe4998cf52fe226fb9e",
    "name": "Leia",
    "dob": "2001-10-08T21:53:00.000Z",
    "loves": [
      "apple",
      "watermelon"
    ],
    "weight": 601,
    "gender": "f",
    "vampires": 33
  },
  {
    "_id": "6324fbe4998cf52fe226fb9f",
    "name": "Pilot",
    "dob": "1997-03-01T13:03:00.000Z",
    "loves": [
      "apple",
      "watermelon"
    ],
    "weight": 650,
    "gender": "m",
    "vampires": 54
  },
  {
    "_id": "6324fbe4998cf52fe226fba0",
    "name": "Nimue",
    "dob": "1999-12-21T00:15:00.000Z",
    "loves": [
      "grape",
      "carrot"
    ],
    "weight": 540,
    "gender": "f"
  },
  {
    "_id": "6324fbe5998cf52fe226fba1",
    "name": "Dunx",
    "dob": "1976-07-19T01:18:00.000Z",
    "loves": [
      "grape",
      "watermelon"
    ],
    "weight": 704,
    "gender": "m",
    "vampires": 165
  }
]
```
and import it to *server.js* using 

```js
var { unicornsJSON } = require('./data.js')
```

---
### Run the server

```js
const express = require('express')

const app = express()
const port = 7000

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
  }
)
```
Make sure the server is running:
![](https://cdn.discordapp.com/attachments/1017862173881544775/1022028353307426866/unknown.png)

- Next, implement the above routes a dummy response for now:
```js
app.get('/api/v1/unicorns', (req, res) => {
  res.send('All the unicorns')
})

app.post('/api/v1/unicorn', (req, res) => {
  res.send('Create a new unicorn')
})

app.get('/api/v1/unicorn/:id', (req, res) => {
  res.send('Get a unicorn')
})

app.patch('/api/v1/unicorn/:id', (req, res) => {
  res.send('Update a unicorn')
})

app.delete('/api/v1/unicorn/:id', (req, res) => {
  res.send('Delete a unicorn')
})

```

---
### Test the server using Thunder Client Extension
Let us test these routes using POSTMAN or in my case, Thunder client in VSCode:
1 - Create a *Collection* of requests
![](https://cdn.discordapp.com/attachments/1017862173881544775/1022029867899944980/unknown.png)

2- Create five *requests* 
![](https://cdn.discordapp.com/attachments/1017862173881544775/1022030105154945036/unknown.png)
Here are the names, types, and attributes of these *requests*
```json
{
  "collectionName": "Unicorns",
  "requests": [
    {
      "name": "getUnicorns",
      "url": "{{URL}}unicorns",
      "method": "GET",
    },
    {
      "name": "createUnicorn",
      "url": "{{URL}}unicorn",
      "method": "POST",
      "body": {
        "type": "json",
        "raw": "{\n  \"x\": 123\n}",
        "form": []
      }
    },
    {
      "name": "getAUnicorn",
      "url": "{{URL}}unicorn/6324fbe4998cf52fe226fb96",
      "method": "GET",
    },
    {
      "name": "updateAUnicorn",
      "url": "{{URL}}unicorn/6324fbe4998cf52fe226fb96",
      "method": "PATCH",
      "body": {
        "type": "json",
        "raw": " {\r\n    \"_id\": \"6324fbe4998cf52fe226fb96\",\r\n    \"name\": \"Horny\",\r\n    \"dob\": \"1992-03-13T15:47:00.000Z\",\r\n    \"loves\": [\r\n      \"carrot\",\r\n      \"papaya\"\r\n    ],\r\n    \"weight\": 600,\r\n    \"gender\": \"m\",\r\n    \"vampires\": 64\r\n  }"
      }
    },
    {
      "name": "deleteAUnicorn",
      "url": "{{URL}}unicorn/6324fbe4998cf52fe226fb96",
      "method": "DELETE"
    }
  ]
}
```

3- Add an `ENV` global variable to match the common prefix of each route - `http://localhost:5000/api/v1/`
![](https://cdn.discordapp.com/attachments/1017862173881544775/1022032688787501086/unknown.png)
![](https://cdn.discordapp.com/attachments/1017862173881544775/1022032813479968789/unknown.png)
You can see that in each of the previous *requests* I have used an `ENV` global variable name `URL`: 
![](https://cdn.discordapp.com/attachments/1017862173881544775/1022033501983354880/unknown.png)
![](https://cdn.discordapp.com/attachments/1017862173881544775/1022033531330891846/unknown.png)
![](https://cdn.discordapp.com/attachments/1017862173881544775/1022033556400250880/unknown.png)
![](https://cdn.discordapp.com/attachments/1017862173881544775/1022033967593041940/unknown.png)
![](https://cdn.discordapp.com/attachments/1017862173881544775/1022033636872175676/unknown.png)

4- Run all the *requests* in the collection and make sure all of them are returning 200 successful responses.
![](https://cdn.discordapp.com/attachments/1017862173881544775/1022034650421530665/unknown.png)

---
### Work on the Express.JS routes
- `app.get('/api/v1/unicorns' ..)` 
```js
app.get('/api/v1/unicorns', (req, res) => {
  res.json(unicornsJSON)
})
```

- `app.get('/api/v1/unicorn/:id', ..)`
```js
app.get('/api/v1/unicorn/:id', (req, res) => {
  var found = false
  for (i = 0; i < unicornsJSON.length; i++) {
    if (unicornsJSON[i]._id == req.params.id) {
      found = true
      break
    }
  }

  if (found) { res.json(unicornsJSON[i]); return }
  res.json({ msg: "not found" })
})
```

- `app.post('/api/v1/unicorn', ..)`
```js
app.use(express.json())
app.post('/api/v1/unicorn', (req, res) => {
  unicornsJSON.push(req.body)
  //update the file
  writeFileAsync('./data.js', JSON.stringify(unicornsJSON), 'utf-8')
    .then(() => { })
    .catch((err) => { console.log(err); })
  res.json(req.body)
})
```
Notice the need of `app.use(express.json())` to access the JSON object in body of the request. `app.use` enable a middleware. We will cover middleware next week. 

- `app.patch('/api/v1/unicorn/:id', ..)`

```js
app.patch('/api/v1/unicorn/:id', (req, res) => {
  unicornsJSON = unicornsJSON.map(({ _id, ...aUnicorn }) => {
    if (_id == req.body._id) {
      console.log("Bingo!");
      return req.body
    } else
      return aUnicorn
  })
  res.send("Updated successfully!")
})
```

- `app.delete('/api/v1/unicorn/:id', ..)`
```js
app.delete('/api/v1/unicorn/:id', (req, res) => {
  unicornsJSON = unicornsJSON.filter((element) => element._id != req.params.id)

  res.send("Deleted successfully?")
})
```
---
## Challenge -  How to read/write the unicorns to a file
So far, all the updates and deletes are stored in memory in that `unicornsJSON` array. Next, let us try to make our changes persistent to mimic a db.

1 - Only store the array in `data.json`:
```json
[
  {
    "_id": "6324fbe4998cf52fe226fb96",
    "name": "Horny",
    "dob": "1992-03-13T15:47:00.000Z",
    "loves": [
      "carrot",
      "papaya"
    ],
    "weight": 600,
    "gender": "m",
    "vampires": 63
  },
  {
    "_id": "6324fbe4998cf52fe226fb97",
    "name": "Aurora",
    "dob": "1991-01-24T21:00:00.000Z",
    "loves": [
      "carrot",
      "grape"
    ],
    "weight": 450,
    "gender": "f",
    "vampires": 43
  },
  {
    "_id": "6324fbe4998cf52fe226fb98",
    "name": "Unicrom",
    "dob": "1973-02-10T06:10:00.000Z",
    "loves": [
      "energon",
      "redbull"
    ],
    "weight": 984,
    "gender": "m",
    "vampires": 182
  },
  {
    "_id": "6324fbe4998cf52fe226fb99",
    "name": "Roooooodles",
    "dob": "1979-08-19T01:44:00.000Z",
    "loves": [
      "apple"
    ],
    "weight": 591,
    "gender": "m",
    "vampires": 99
  },
  {
    "_id": "6324fbe4998cf52fe226fb9a",
    "name": "Solnara",
    "dob": "1985-07-04T09:01:00.000Z",
    "loves": [
      "apple",
      "carrot",
      "chocolate"
    ],
    "weight": 550,
    "gender": "f",
    "vampires": 80
  },
  {
    "_id": "6324fbe4998cf52fe226fb9b",
    "name": "Ayna",
    "dob": "1998-03-07T16:30:00.000Z",
    "loves": [
      "strawberry",
      "lemon"
    ],
    "weight": 733,
    "gender": "f",
    "vampires": 40
  },
  {
    "_id": "6324fbe4998cf52fe226fb9c",
    "name": "Kenny",
    "dob": "1997-07-01T17:42:00.000Z",
    "loves": [
      "grape",
      "lemon"
    ],
    "weight": 690,
    "gender": "m",
    "vampires": 39
  },
  {
    "_id": "6324fbe4998cf52fe226fb9d",
    "name": "Raleigh",
    "dob": "2005-05-03T07:57:00.000Z",
    "loves": [
      "apple",
      "sugar"
    ],
    "weight": 421,
    "gender": "m",
    "vampires": 2
  },
  {
    "_id": "6324fbe4998cf52fe226fb9e",
    "name": "Leia",
    "dob": "2001-10-08T21:53:00.000Z",
    "loves": [
      "apple",
      "watermelon"
    ],
    "weight": 601,
    "gender": "f",
    "vampires": 33
  },
  {
    "_id": "6324fbe4998cf52fe226fb9f",
    "name": "Pilot",
    "dob": "1997-03-01T13:03:00.000Z",
    "loves": [
      "apple",
      "watermelon"
    ],
    "weight": 650,
    "gender": "m",
    "vampires": 54
  },
  {
    "_id": "6324fbe4998cf52fe226fba0",
    "name": "Nimue",
    "dob": "1999-12-21T00:15:00.000Z",
    "loves": [
      "grape",
      "carrot"
    ],
    "weight": 540,
    "gender": "f"
  },
  {
    "_id": "6324fbe5998cf52fe226fba1",
    "name": "Dunx",
    "dob": "1976-07-19T01:18:00.000Z",
    "loves": [
      "grape",
      "watermelon"
    ],
    "weight": 704,
    "gender": "m",
    "vampires": 165
  }
]
```

2- Comment out the following line
```js
// var { unicornsJSON } = require('./data.js')
```

3- Read the `unicornsJSON` object in the `listen` method:
```js
const { writeFile, readFile } = require('fs')
const util = require('util')
const writeFileAsync = util.promisify(writeFile)
const readFileAsync = util.promisify(readFile)
var unicornsJSON = []

app.listen(port, async () => {
  try {
    unicornsJSON = await readFileAsync('./data.json', 'utf-8')
    if (!unicornsJSON) {
      console.log("Could not read the file");
      return
    }
    unicornsJSON = JSON.parse(unicornsJSON)
    console.log(unicornsJSON);
  } catch (error) {
    console.log(error);
  }

  console.log(`Example app listening on port ${port}`)
})
```

4 - Update the file in the `POST`, `PATCH` and `DELETE` routes:
```js
  //update the file
  writeFileAsync('./data.json', JSON.stringify(unicornsJSON), 'utf-8')
    .then(() => { })
    .catch((err) => { console.log(err); })
```

5- Test again all the *requests*.

---
# Deploy your site to Heroku
- Requirements 
  - [Git installing](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
  - [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli)

Create an account on Heroku, [install the Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli), and make sure you have less than five app.

Also, you need git cli to be installed on your shell.

First change the listening port to

```js
app.listen(process.env.PORT || 5000, function (err) {
    if (err)
        console.log(err);
})
```
so Heroku can set a port number dynamically.

In the terminal in VSCode, execute the following  

```bash
git init
```
to initialize  a repository.

and

```bash
git add .
```
to add all the files to the repository.

and


```shell
git commit -m "my first commit"
```
to commit.

And

```shell
heroku login
```
which is going to prompt you to login using the browser.

Next type,
```shell
heroku create
```
to create a remote repo on Heroku site.

And

```shell
git push heroku master
```

to sync and push local changes to the remote repo hosted on Heroku.com.


---
# Challenges
 Can you add the followings routes to your server to set, add an item, or remove an item to/from the *loves* array for a unicorn:
- `app.patch('/api/v1/unicornNewLovesFood/:id/', ()=>{})` and pass the new array food using a JSON object in the body of PATCH HTTP request?
- `app.patch('/api/v1/unicornAddLovesFood/:id/:item', ()=>{})` and pass the food item as a URL parameter of the PATCH HTTP request?
- `app.patch('/api/v1/unicornRemoveLovesFood/:id/:item', ()=>{})` and pass the array food item to be removed as a URL parameter of the PATCH HTTP request?

<details>
<summary>
Solution
</summary>

```js
app.patch('/api/v1/unicornNewLovesFood/:id/', (req, res) => {
  unicornsJSON = unicornsJSON.map(({ _id, loves, ...rest }) => {
    if (_id == req.params.id) {
      return { _id, loves: req.body.loves, ...rest }
    } else
      return { _id, loves, ...rest }
  })

  //update the file
  writeFileAsync('./data.json', JSON.stringify(unicornsJSON), 'utf-8')
    .then(() => { })
    .catch((err) => { console.log(err); })

  res.send("Updated successfully!")
})




app.patch('/api/v1/unicornAddLovesFood/:id/', (req, res) => {
  unicornsJSON = unicornsJSON.map(({ _id, loves, ...rest }) => {
    if (_id == req.params.id) {
      return { _id, "loves": [...loves, ...req.body.newLoves], ...rest }
    } else
      return { _id, loves, ...rest }
  })

  //update the file
  writeFileAsync('./data.json', JSON.stringify(unicornsJSON), 'utf-8')
    .then(() => { })
    .catch((err) => { console.log(err); })

  res.send("Updated successfully!")
})

app.patch('/api/v1/unicornRemoveLovesFood/:id/:item', (req, res) => {
  unicornsJSON = unicornsJSON.map(({ _id, loves, ...rest }) => {
    if (_id === req.params.id)
      loves = loves.filter(anItem => anItem !== req.params.item)
    return { _id, loves, ...rest }
  })
  //update the file
  writeFileAsync('./data.json', JSON.stringify(unicornsJSON), 'utf-8')
    .then(() => { })
    .catch((err) => { console.log(err); })
  res.send("Updated successfully!")
})

```
</details>



<details>
<summary>
Requests
</summary>

```js
{
  "client": "Thunder Client",
  "collectionName": "unicornLovesFood",
  "dateExported": "2022-09-29T00:08:14.791Z",
  "version": "1.1",
  "folders": [],
  "requests": [
    {
      "_id": "3aa06fc1-9f40-45ce-9e0a-b4685230357a",
      "colId": "d030e77e-9524-48b8-b17e-222617e7f681",
      "containerId": "",
      "name": "unicornNewLovesFood",
      "url": "{{URL}}unicornNewLovesFood/6324fbe4998cf52fe226fb97",
      "method": "PATCH",
      "sortNum": 10000,
      "created": "2022-09-28T15:15:21.804Z",
      "modified": "2022-09-28T15:52:01.781Z",
      "headers": [],
      "params": [],
      "body": {
        "type": "json",
        "raw": " {\n    \"loves\": [\n      \"orange\",\n      \"apple\"\n    ]\n  }",
        "form": []
      },
      "tests": []
    },
    {
      "_id": "45c383a0-211d-4ac5-b214-916bfa647a35",
      "colId": "d030e77e-9524-48b8-b17e-222617e7f681",
      "containerId": "",
      "name": "unicornAddLovesFood",
      "url": "{{URL}}unicornAddLovesFood/6324fbe4998cf52fe226fb97",
      "method": "PATCH",
      "sortNum": 20000,
      "created": "2022-09-28T15:18:29.449Z",
      "modified": "2022-09-28T16:00:42.270Z",
      "headers": [],
      "params": [],
      "body": {
        "type": "json",
        "raw": " {\n    \"newLoves\": [\n      \"carrot\",\n      \"tomato\"\n    ]\n  }",
        "form": []
      },
      "tests": []
    },
    {
      "_id": "3d64884e-8175-49ea-8609-2ff947fba3a8",
      "colId": "d030e77e-9524-48b8-b17e-222617e7f681",
      "containerId": "",
      "name": "unicornRemoveLovesFood",
      "url": "{{URL}}unicornRemoveLovesFood/6324fbe4998cf52fe226fb97/carrot",
      "method": "PATCH",
      "sortNum": 30000,
      "created": "2022-09-28T15:27:59.687Z",
      "modified": "2022-09-28T16:12:52.816Z",
      "headers": [],
      "params": [],
      "tests": []
    }
  ]
}
```
</details>


---
# Food for thought 🍎
- HTTP PATCH vs PUT
