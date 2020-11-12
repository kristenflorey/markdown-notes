# Sequelize
- Sequelize provides utilities for generating migrations, models, and seed files. They are exposed through the `sequelize-cli` command.

### Command Line
##### Initialize Project
  ```
  npm install sequelize sequelize-cli pg
  npx sequelize-cli init
  ```
- You must create a database user, update the `config/config.json` file to match your database settings to complete the initialization process.

##### Create Database
  ```
  npx sequelize-cli db:create
  ```
#### Seeds
##### Generate a new seed file
```
npx sequelize-cli seed:generate --name <descriptiveName>
```

##### Run all pending seeds
```
npx sequelize-cli db:seed:all
```
##### Rollback Seeds
- ###### One seed
  ```
  npx sequelize-cli db:seed:undo
  ```
- ###### All seeds
  ```
  npx sequelize-cli db:seed:undo:all
  ```

#### Migrations
##### Generate a model and its migration
```
npx sequelize-cli model:generate --name <ModelName> --attributes<column1>:<type>,<column2>:<type>,...
```

##### Run all pending migrations
  ```
  npx sequelize-cli db:migrate
  ```


##### Rollback Migrations
- ###### One migration
  ```
  npx sequelize-cli db:migrate:undo
  ```
- ###### All migrations
  ```
  npx sequelize-cli db:migrate:undo:all
  ```
#### Javascript SQL Functions
##### Connecting to a Database
```js
const { Sequelize } = require('sequelize');

// Option 1: Passing a connection URI
const sequelize = new Sequelize('sqlite::memory:') // Example for sqlite
const sequelize = new Sequelize('postgres://user:pass@example.com:5432/dbname') // Example for postgres

// Option 2a: Passing parameters separately (sqlite)
const sequelize = new Sequelize({
  dialect: 'sqlite',
  storage: 'path/to/database.sqlite'
});
// Option 2b: Passing parameters separately (other dialects)
const sequelize = new Sequelize('database', 'username', 'password', {
  host: 'localhost',
  dialect: /* one of 'mysql' | 'mariadb' | 'postgres' | 'mssql' */
});
```
##### Testing the Connection

```js
try {
  await sequelize.authenticate();
  console.log('Connection has been established successfully.');
} catch (error) {
  console.error('Unable to connect to the database:', error);
}
```
- ###### Closing the Connection
  ```js
  sequelize.close()
  ```

##### Create a Table
- Usually used in the `up()` method
```js
return queryInterface.createTable(<TableName>, {
  <columnName>: {        
    type: Sequelize.<type>,        
    allowNull: <true|false>,        
    unique: <true|false>,        
    references: {            
      model: {                
        tableName: <TableName>             
      }        
    }
  }
});    
```
##### Delete Table
- Usually used in the `down()` method
```js
return queryInterface.dropTable(<TableName>);
```
  - ###### To drop the table related to a model:
    ```js
    await User.drop();
    ```
  - ###### To drop all tables:
    ```js
    await sequelize.drop();
    ```
##### Adding a column
```js
return queryInteface.addColumn(<TableName>, <columnName>: {    
  type: Sequelize.<type>,    
  allowNull: <true|false>,    
  unique: <true|false>,    
  references: {
    model: <TableName>
    },
});
```
##### Removing a column
```js
return queryInterface.removeColumn(<TableName>, <columnName>);
```
---
### Models
- A Model represents a table in the database. Instances of this class represent a database row.
  - Model instances operate with the concept of a dataValues property, which stores the actual values represented by the instance. By default, the values from dataValues can also be accessed directly from the Instance, that is:
    ```js
    instance.field
    // is the same as
    instance.get('field')
    // is the same as
    instance.getDataValue('field')
    ```
  - However, if getters and/or setters are defined for field they will be invoked, instead of returning the value from `dataValues`.
  - Accessing properties directly or using get is preferred for regular use, `getDataValue` should only be used for custom getters.
  - See [Public Methods](https://sequelize.org/master/class/lib/model.js~Model.html)
#### Model Basics
- Models are the essence of Sequelize.
- A model is an abstraction that represents a table in your database.
  - In Sequelize, it is a class that extends Model.
- The model tells Sequelize several things about the entity it represents, such as:
  - the name of the table in the database
  - which columns it has (and their data types)
##### Naming Models
- A model in Sequelize has a name.
  - This name does not have to be the same name of the table it represents in the database.
  - Usually, models have singular names (such as `User`) while tables have pluralized names (such as `Users`), although this is fully configurable.
##### Defining a Model
- Models can be defined in two equivalent ways in Sequelize:
  - Calling `sequelize.define(modelName, attributes, options)`
  - Extending Model and calling `init(attributes, options)`
- After a model is defined, it is available within sequelize.models by its model name.

###### Using `sequelize.define`
```js
const { Sequelize, DataTypes } = require('sequelize');
const sequelize = new Sequelize('sqlite::memory:');

const User = sequelize.define('User', {
  // Model attributes are defined here
  firstName: {
    type: DataTypes.STRING,
    allowNull: false
  },
  lastName: {
    type: DataTypes.STRING
    // allowNull defaults to true
  }
}, {
  // Other model options go here
});

// `sequelize.define` also returns the model
console.log(User === sequelize.models.User); // true
```

##### Synchronizing a Model  
- In the case where the table doesn't even exist in the database or if it exists, but it has different columns, less columns, or any other difference, models can be synchronized by calling `model.sync(options)`, an asynchronous function (that returns a Promise)
- With this call, Sequelize will automatically perform an SQL query to the database.

| Function                     | Action                                                                                                                                                                                                      |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `User.sync()`                | This creates the table if it doesn't exist (and does nothing if it already exists)                                                                                                                          |
| `User.sync({ force: true })` | This creates the table, dropping it first if it already existed                                                                                                                                             |
| `User.sync({ alter: true })` | This checks what is the current state of the table in the database (which columns it has, what are their data types, etc), and then performs the necessary changes in the table to make it match the model. |


##### Promises and `async`/`await`
- Most of the methods provided by Sequelize are asynchronous and therefore return Promises.
- They are all Promises , so you can use the Promise API (for example, using then, catch, finally) out of the box.
- Of course, using async and await works normally as well.

#### Model Instances
