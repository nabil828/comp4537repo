# Lab 4 - RESTful API Server - Round II (DB)

## Goals
- To build a RESTful API server connected to MongoDb database.
- Test using POSTMAN/Thunder Client
- To deploy server on Heroku  
- To test mongoose queries

## Keywords
- Mongoose
  - Connection, Schema, Model, Query

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


Table of Contents
=================

* [Lab 4 - RESTful API Server - Round II (DB)](#lab-4---restful-api-server---round-ii-db)
   * [Goals](#goals)
   * [Keywords](#keywords)
* [Table of Contents](#table-of-contents)
   * [Next lab: RESTful API Server - Round III](#next-lab-restful-api-server---round-iii)
   * [Steps](#steps)
      * [Create a Package](#create-a-package)
      * [Create the unicorns DB](#create-the-unicorns-db)
      * [Run the server](#run-the-server)
      * [Test the server using Thunder Client Extension](#test-the-server-using-thunder-client-extension)
      * [Add a Schema and a Model](#add-a-schema-and-a-model)
      * [Work on the Express.JS routes](#work-on-the-expressjs-routes)
* [Deploy your site to Heroku](#deploy-your-site-to-heroku)
* [Host DB on MongoDB Atlas](#host-db-on-mongodb-atlas)
* [Challenges](#challenges)


---
## Next lab: RESTful API Server - Round III
Next week, we will add sessions to the server.

---
## Steps
### Create a Package
- Create a Node.JS package and install express.js
- Add the following routes stubs to your file:

```js
// app.get('/api/v2/unicorns')           // - get all the unicorns
// app.post('/api/v2/unicorn')          // - create a new unicorn
// app.get('/api/v2/unicorn/:id')       // - get a unicorn
// app.patch('/api/v2/unicorn/:id')     // - update a unicorn
// app.delete('/api/v2/unicorn/:id')       // - delete unicorn
```

---
### Create the `unicorns` DB 
- create a new mongodb * with the following `insert` mongodb functions:

```js
db.unicorns.insert({name: 'Horny',
		dob: new Date(1992,2,13,7,47),
		loves: ['carrot','papaya'],
		weight: 600,
		gender: 'm',
		vampires: 63});
	db.unicorns.insert({name: 'Aurora',
		dob: new Date(1991, 0, 24, 13, 0),
		loves: ['carrot', 'grape'],
		weight: 450,
		gender: 'f',
		vampires: 43});
	db.unicorns.insert({name: 'Unicrom',
		dob: new Date(1973, 1, 9, 22, 10),
		loves: ['energon', 'redbull'],
		weight: 984,
		gender: 'm',
		vampires: 182});
	db.unicorns.insert({name: 'Roooooodles',
		dob: new Date(1979, 7, 18, 18, 44),
		loves: ['apple'],
		weight: 575,
		gender: 'm',
		vampires: 99});
	db.unicorns.insert({name: 'Solnara',
		dob: new Date(1985, 6, 4, 2, 1),
		loves:['apple', 'carrot',
			'chocolate'],
		weight:550,
		gender:'f',
		vampires:80});
	db.unicorns.insert({name:'Ayna',
		dob: new Date(1998, 2, 7, 8, 30),
		loves: ['strawberry', 'lemon'],
		weight: 733,
		gender: 'f',
		vampires: 40});
	db.unicorns.insert({name:'Kenny',
		dob: new Date(1997, 6, 1, 10, 42),
		loves: ['grape', 'lemon'],
		weight: 690,
		gender: 'm',
		vampires: 39});
	db.unicorns.insert({name: 'Raleigh',
		dob: new Date(2005, 4, 3, 0, 57),
		loves: ['apple', 'sugar'],
		weight: 421,
		gender: 'm',
		vampires: 2});
	db.unicorns.insert({name: 'Leia',
		dob: new Date(2001, 9, 8, 14, 53),
		loves: ['apple', 'watermelon'],
		weight: 601,
		gender: 'f',
		vampires: 33});
	db.unicorns.insert({name: 'Pilot',
		dob: new Date(1997, 2, 1, 5, 3),
		loves: ['apple', 'watermelon'],
		weight: 650,
		gender: 'm',
		vampires: 54});
	db.unicorns.insert({name: 'Nimue',
		dob: new Date(1999, 11, 20, 16, 15),
		loves: ['grape', 'carrot'],
		weight: 540,
		gender: 'f'});
	db.unicorns.insert({name: 'Dunx',
		dob: new Date(1976, 6, 18, 18, 18),
		loves: ['grape', 'watermelon'],
		weight: 704,
		gender: 'm',
		vampires: 165});


```

---
### Run the server

```js
const express = require('express')
const mongoose = require('mongoose')

const app = express()
const port = 5000

app.listen(port, async () => {
  try {
    await mongoose.connect('mongodb://localhost:27017/test')
  } catch (error) {
    console.log('db error');
  }
  console.log(`Example app listening on port ${port}`)
}
)
```
Make sure the server is running:
![](https://cdn.discordapp.com/attachments/1017862173881544775/1024697061024739338/unknown.png)

- Next, implement the above routes a dummy response for now:
```js
app.get('/api/v2/unicorns', (req, res) => {
  res.send('All the unicorns')
})

app.post('/api/v2/unicorn', (req, res) => {
  res.send('Create a new unicorn')
})

app.get('/api/v2/unicorn/:id', (req, res) => {
  res.send('Get a unicorn')
})

app.patch('/api/v2/unicorn/:id', (req, res) => {
  res.send('Update a unicorn')
})

app.delete('/api/v2/unicorn/:id', (req, res) => {
  res.send('Delete a unicorn')
})

```

---
### Test the server using Thunder Client Extension
<details>
<summary>
Collapsed. Same as last lab. 
</summary>

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
![v2](https://cdn.discordapp.com/attachments/1017862173881544775/1024696620241125396/unknown.png)
You can see that in each of the previous *requests* I have used an `ENV` global variable name `URL`: 
![](https://cdn.discordapp.com/attachments/1017862173881544775/1022033501983354880/unknown.png)
![](https://cdn.discordapp.com/attachments/1017862173881544775/1022033531330891846/unknown.png)
![](https://cdn.discordapp.com/attachments/1017862173881544775/1022033556400250880/unknown.png)
![](https://cdn.discordapp.com/attachments/1017862173881544775/1022033967593041940/unknown.png)
![](https://cdn.discordapp.com/attachments/1017862173881544775/1022033636872175676/unknown.png)

4- Run all the *requests* in the collection and make sure all of them are returning 200 successful responses.
![](https://cdn.discordapp.com/attachments/1017862173881544775/1022034650421530665/unknown.png)
</details>

---
### Add a Schema and a Model 

```js

const { Schema } = mongoose;

const unicornSchema = new Schema({
  "name": String, // String is shorthand for {type: String}
  "weight": Number,
  "loves": [String],
  "gender": {
    enum: ["f", "m"]
  },
  "vampires": Number,
  "dob": Date
});

const unicornModel = mongoose.model('unicorns', unicornSchema); // unicorns is the name of the collection in db

``` 
### Work on the Express.JS routes
- `app.get('/api/v2/unicorns' ..)` 
```js
app.get('/api/v2/unicorns', (req, res) => {
  unicornModel.find({})
    .then(docs => {
      console.log(docs)
      res.json(docs)
    })
    .catch(err => {
      console.error(err)
      res.json({ msg: "db reading .. err.  Check with server devs" })
    })
  // res.json(unicornsJSON)
})
```

- `app.get('/api/v2/unicorn/:id', ..)`

```js
app.get('/api/v2/unicorn/:id', (req, res) => {
  // var found = false
  // for (i = 0; i < unicornsJSON.length; i++) {
  //   if (unicornsJSON[i]._id == req.params.id) {
  //     found = true
  //     break
  //   }
  // }
  // if (found) { res.json(unicornsJSON[i]); return }
  // res.json({ msg: "not found" })
  console.log(req.params.id);
  unicornModel.find({ _id: mongoose.Types.ObjectId(`${req.params.id}`) })
    .then(doc => {
      console.log(doc)
      res.json(doc)
    })
    .catch(err => {
      console.error(err)
      res.json({ msg: "db reading .. err.  Check with server devs" })
    })
})
```

- `app.post('/api/v2/unicorn', ..)`

```js
app.use(express.json())
app.post('/api/v2/unicorn', (req, res) => {
  // - create a new unicorn

  // unicornsJSON.push(req.body)
  //update the file
  // writeFileAsync('./data.js', JSON.stringify(unicornsJSON), 'utf-8')
  //   .then(() => { })
  //   .catch((err) => { console.log(err); })

  unicornModel.create(req.body, function (err) {
    if (err) console.log(err);
    // saved!
  });
  res.json(req.body)
})  
```
Notice the need of `app.use(express.json())` to access the JSON object in body of the request. `app.use` enable a middleware. We will cover middleware next week. 

- `app.patch('/api/v2/unicorn/:id', ..)`

```js
app.patch('/api/v2/unicorn/:id', (req, res) => {
  // - update a unicorn

  // unicornsJSON = unicornsJSON.map(({ _id, ...aUnicorn }) => {
  //   // console.log(req.body);
  //   if (_id == req.body._id) {
  //     console.log("Bingo!");
  //     return req.body
  //   } else
  //     return aUnicorn
  // })
  // console.log(unicornsJSON);


  //update the file
  // writeFileAsync('./data.js', JSON.stringify(unicornsJSON), 'utf-8')
  //   .then(() => { })
  //   .catch((err) => { console.log(err); })
  // console.log(req.body);
  const { _id, ...rest } = req.body;
  unicornModel.updateOne({ _id: mongoose.Types.ObjectId(req.params.id) }, rest, function (err, res) {
    // Updated at most one doc, `res.nModified` contains the number
    // of docs that MongoDB updated
    if (err) console.log(err)
    console.log(res)
  });

  res.send("Updated successfully!")
})
```

- `app.delete('/api/v2/unicorn/:id', ..)`

```js
app.delete('/api/v2/unicorn/:id', (req, res) => {
  // - delete a unicorn
  // unicornsJSON = unicornsJSON.filter((element) => element._id != req.params.id)

  // //update the file
  // writeFileAsync('./data.js', JSON.stringify(unicornsJSON), 'utf-8')
  //   .then(() => { })
  //   .catch((err) => { console.log(err); })
  unicornModel.deleteOne({ _id: mongoose.Types.ObjectId(req.params.id) }, function (err, result) {
    if (err) console.log(err);
    console.log(result);
  });

  res.send("Deleted successfully?")
})
```

---
# Deploy your site to Heroku
[Check lab 3 for instructions](https://github.com/nabil828/comp4537repo/tree/main/Labs/Lab%203%20-%20RESTful%20API%20server%20-%20Round%20I%20(files))

# Host DB on MongoDB Atlas
> MongoDB Atlas: Deploy and scale a MongoDB cluster in the cloud with just a few clicks:
- [Create an account and sign in ](https://cloud.mongodb.com/)
- Create a cluster
![create a cluster](https://cdn.discordapp.com/attachments/1017862173881544775/1024803927193030656/unknown.png)

- Make sure it is shared cluster
![Shared cluster](https://cdn.discordapp.com/attachments/1017862173881544775/1024804180642250864/unknown.png)


- Browse for Collections
![Browse Collections](https://cdn.discordapp.com/attachments/1017862173881544775/1024804348259213363/unknown.png)

- Create a DB if there is no default one
![Create a DB if there is no default one](https://cdn.discordapp.com/attachments/1017862173881544775/1024804493122089001/unknown.png)

- Add a collection
![Add a collection](https://cdn.discordapp.com/attachments/1017862173881544775/1024804612361965620/unknown.png)

- Now we have a collection inside a db
![Now we have a collection inside a db](https://cdn.discordapp.com/attachments/1017862173881544775/1024804750740422756/unknown.png)

- Add unicorns
![Add documents](https://cdn.discordapp.com/attachments/1017862173881544775/1024805019670822942/unknown.png)

- Add a user
![Add a user](https://cdn.discordapp.com/attachments/1017862173881544775/1024805197454790656/unknown.png)

- Add!
![](https://cdn.discordapp.com/attachments/1017862173881544775/1024805223904063559/unknown.png)

- Add a autogenerated password
![](https://cdn.discordapp.com/attachments/1017862173881544775/1024805279520526408/unknown.png)

- readWriteAnyDatabase permission 
![readWriteAnyDatabase@admin
](https://cdn.discordapp.com/attachments/1017862173881544775/1024805308972925029/unknown.png)

- Whitelist all the IPs
![Whitelist](https://cdn.discordapp.com/attachments/1017862173881544775/1024805333115342978/unknown.png)

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


app.patch('/api/v2/unicornNewLovesFood/:id/', (req, res) => {
  unicornModel.updateOne({ _id: mongoose.Types.ObjectId(req.params.id) }, req.body, function (err, res) {
    // Updated at most one doc, `res.nModified` contains the number
    // of docs that MongoDB updated
    if (err) console.log(err)
    console.log(res)
  });

  res.send("Updated successfully!")
})

app.patch('/api/v2/unicornAddLovesFood/:id/', (req, res) => {
  unicornModel.updateOne({ _id: mongoose.Types.ObjectId(req.params.id) }, {
    $push: {
      loves: req.body.newLoves
    }
  }, function (err, res) {
    // Updated at most one doc, `res.nModified` contains the number
    // of docs that MongoDB updated
    if (err) console.log(err)
    console.log(res)
  });
  res.send("Updated successfully!")
})

app.patch('/api/v2/unicornRemoveLovesFood/:id/:item', (req, res) => {
  unicornModel.updateOne({ _id: mongoose.Types.ObjectId(req.params.id) }, {
    $pull: {
      loves: req.params.item
    }
  }, function (err, res) {
    // Updated at most one doc, `res.nModified` contains the number
    // of docs that MongoDB updated
    if (err) console.log(err)
    console.log(res)
  });
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

