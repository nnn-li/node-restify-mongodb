## node-restify-mongodb

轻量级 的 nodejs RESTful applications

- restify



## Using the Generated Application
Import sample widget documents into MongoDB from the supplied 'data/widgets.json' file
``` bash
# import to local development environment
grunt mongoimport --verbose
  
# import to production environment db instance
NODE_ENV=production grunt mongoimport --verbose
```

Start the application
``` bash
npm run
```

To test the application, the sample documents must be imported into MongoDB (see above), and the application must be running (see above)
``` bash
npm test
```

Test the running application by cURLing the '/widgets' endpoint
``` bash
curl -X GET -H "Accept: application/json" "http://localhost:3000/widgets"
```
For a better output, try
``` bash
npm install -g json
curl -X GET -H "Accept: application/json" "http://localhost:3000/widgets" --silent | json
curl -X GET -H "Accept: application/json" "http://localhost:3000/widgets/SVHXPAWEOD" --silent | json
```



#### API Endpoints
The current API endpoints, include the following
``` javascript
# widget resources
var PATH = '/widgets';
server.get({path: PATH, version: VERSION}, findDocuments);
server.get({path: PATH + '/:product_id', version: VERSION}, findOneDocument);
server.post({path: PATH, version: VERSION}, createDocument);
server.put({path: PATH, version: VERSION}, updateDocument);
server.del({path: PATH + '/:product_id', version: VERSION}, deleteDocument);
  
# utility resources
var PATH = '/utils';
server.get({path: PATH + '/ping', version: VERSION}, ping);
server.get({path: PATH + '/health', version: VERSION}, health);
server.get({path: PATH + '/info', version: VERSION}, information);
server.get({path: PATH + '/config', version: VERSION}, configuraton);
server.get({path: PATH + '/env', version: VERSION}, environment);
```

#### Widget
The basic 'widget' object is used throughout, to demonstrate Mongoose's
 [Model](http://mongoosejs.com/docs/models.html) and [Schema](http://mongoosejs.com/docs/guide.html)
``` json
{
  "product_id": "4OZNPBMIDR",
  "name": "Fapster",
  "color": "Orange",
  "size": "Medium",
  "price": "29.99",
  "inventory": 5
}
```

#### MongoDB
To access the application's MongoDB database with sample documents
```
mongo
 > show dbs
 > use node-restify-mongodb-development
 > show tables
 > db.widgets.find()
  { "_id" : ObjectId("574cf9bb0f515d7c67a87026"), "product_id" : "4OZNPBMIDR", "name" : "Fapster", "color" : "Orange", "size" : "Medium", "price" : "29.99", "inventory" : 5 }
  { "_id" : ObjectId("574cf9bb0f515d7c67a87027"), "product_id" : "SVHXPAWEOD", "name" : "Voonex", "color" : "Green", "size" : "Medium", "price" : "$10.99", "inventory" : 50 }
  { "_id" : ObjectId("574cf9bb0f515d7c67a87028"), "product_id" : "3YIRGZ6TDW", "name" : "Groopster", "color" : "Yellow", "size" : "Large", "price" : "$99.95", "inventory" : 100 }
  { "_id" : ObjectId("574cf9bb0f515d7c67a87029"), "product_id" : "6T2HC5MIZ9", "name" : "Chaintwist", "color" : "Purple", "size" : "Tiny", "price" : "$99.95", "inventory" : 15 }
  { "_id" : ObjectId("574cf9bb0f515d7c67a8702a"), "product_id" : "ERZ1RMJFR3", "name" : "Glozzom", "color" : "Red", "size" : "Huge", "price" : "$199.98", "inventory" : 35 }
  { "_id" : ObjectId("574cf9bb0f515d7c67a8702b"), "product_id" : "N43WV5234S", "name" : "Zapster", "color" : "Green", "size" : "Tiny", "price" : "$17.49", "inventory" : 65 }
  { "_id" : ObjectId("574cf9bb0f515d7c67a8702c"), "product_id" : "0BVCLPDZ42", "name" : "Chaintwist", "color" : "Blue", "size" : "Medium", "price" : "$89.95", "inventory" : 55 }
  { "_id" : ObjectId("574cf9bb0f515d7c67a8702d"), "product_id" : "N212QZOD9B", "name" : "Pentwist", "color" : "Yellow", "size" : "Huge", "price" : "$159.98", "inventory" : 95 }
  { "_id" : ObjectId("574cf9bb0f515d7c67a8702e"), "product_id" : "RTHGP1FCGN", "name" : "Reflupper", "color" : "Red", "size" : "Large", "price" : "$12.95", "inventory" : 25 }
  { "_id" : ObjectId("574cf9bb0f515d7c67a8702f"), "product_id" : "GKO1SFX04M", "name" : "Jukelox", "color" : "Blue", "size" : "Small", "price" : "$25.49", "inventory" : 75 }
```

#### Environmental Variables
The application uses the following environment variables and defaults, which are found in the 'config/config.js' file.
``` javascript
var NODE_ENV   = process.env.NODE_ENV   || 'development';
var NODE_HOST  = process.env.NODE_HOST  || '127.0.0.1';
var NODE_PORT  = process.env.NODE_PORT  || 3000;
var MONGO_HOST = process.env.MONGO_HOST || '127.0.0.1';
var MONGO_PORT = process.env.MONGO_PORT || 27017;
var LOG_LEVEL  = process.env.LOG_LEVEL  || 'info';
var APP_NAME   = 'node-restify-mongodb-';
```