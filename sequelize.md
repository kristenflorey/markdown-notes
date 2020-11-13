# Sequelize
- Sequelize provides utilities for generating migrations, models, and seed files. They are exposed through the `sequelize-cli` command.

## Command Line
#### Initialize Project
  ```
  npm install sequelize sequelize-cli pg
  npx sequelize-cli init
  ```
- You must create a database user, update the `config/config.json` file to match your database settings to complete the initialization process.

#### Create Database
  ```
  npx sequelize-cli db:create
  ```
### Seeds
#### Generate a new seed file
```
npx sequelize-cli seed:generate --name <descriptiveName>
```

#### Run all pending seeds
```
npx sequelize-cli db:seed:all
```
#### Rollback Seeds
- ##### One seed
  ```
  npx sequelize-cli db:seed:undo
  ```
- ##### All seeds
  ```
  npx sequelize-cli db:seed:undo:all
  ```

### Migrations
#### Generate a model and its migration
```
npx sequelize-cli model:generate --name <ModelName> --attributes<column1>:<type>,<column2>:<type>,...
```

#### Run all pending migrations
  ```
  npx sequelize-cli db:migrate
  ```


#### Rollback Migrations
- ##### One migration
  ```
  npx sequelize-cli db:migrate:undo
  ```
- ##### All migrations
  ```
  npx sequelize-cli db:migrate:undo:all
  ```
## Javascript SQL Functions
#### Connecting to a Database
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
#### Testing the Connection

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

#### Create a Table
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
#### Delete Table
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
#### Adding a column
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
#### Removing a column
```js
return queryInterface.removeColumn(<TableName>, <columnName>);
```
---
## Models
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
### Model Basics
- Models are the essence of Sequelize.
- A model is an abstraction that represents a table in your database.
  - In Sequelize, it is a class that extends Model.
- The model tells Sequelize several things about the entity it represents, such as:
  - the name of the table in the database
  - which columns it has (and their data types)
#### Naming Models
- A model in Sequelize has a name.
  - This name does not have to be the same name of the table it represents in the database.
  - Usually, models have singular names (such as `User`) while tables have pluralized names (such as `Users`), although this is fully configurable.
#### Defining a Model
- Models can be defined in two equivalent ways in Sequelize:
  - Calling `sequelize.define(modelName, attributes, options)`
  - Extending Model and calling `init(attributes, options)`
- After a model is defined, it is available within sequelize.models by its model name.

##### Using `sequelize.define`
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

#### Synchronizing a Model  
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

## Queries
#### INSERT queries
- The `Model.create()` method is a shorthand for building an unsaved instance with `Model.build()` and saving the instance with `instance.save()`.
```js
// Create a new user
const jane = await User.create({ firstName: "Jane", lastName: "Doe" });
console.log("Jane's auto-generated ID:", jane.id);
```
- ##### Creating in bulk
  - Sequelize provides the `Model.bulkCreate` method to allow creating multiple records at once, with only one query.
  - The usage of `Model.bulkCreate` is very similar to `Model.create`, by receiving an array of objects instead of a single object.
  ```js
  const create = await bulkCreate(records: Array, options: object): Promise<Array<Model>>
  ```
  - by default, `bulkCreate` does not run validations on each object that is going to be created (which create does).
    - To make `bulkCreate` run these validations as well, you must pass the `validate: true` option. This will decrease performance.

#### SELECT queries
- You can read the whole table from the database with the findAll method:
```js
// Find all users
const users = await User.findAll();
console.log(users.every(user => user instanceof User)); // true
console.log("All users:", JSON.stringify(users, null, 2));
```
```
SELECT * FROM ...
```
- ###### Specifying attributes for SELECT queries:
  ```js
  Model.findAll({
    attributes: ['foo', 'bar']
  });
  ```
  ```
  SELECT foo, bar FROM ...
  ```
- ###### Attributes can be renamed using a nested array:
  ```js
  Model.findAll({
    attributes: ['foo', ['bar', 'baz'], 'qux']
  });
  ```
  ```
  SELECT foo, bar AS baz, qux FROM ...
  ```
- ###### Applying WHERE clause
  - The where option is used to filter the query. There are lots of operators to use for the where clause, available as Symbols from [Operator Symbols](https://sequelize.org/master/variable/index.html#static-variable-Op).
  ```js
  Post.findAll({
    where: {
      authorId: 2
    }
  });
  // SELECT * FROM post WHERE authorId = 2
  ```
#### UPDATE queries
```js
// Change everyone without a last name to "Doe"
await User.update({ lastName: "Doe" }, {
  where: {
    lastName: null
  }
});
```
#### DELETE queries
```js
// Delete everyone named "Jane"
await User.destroy({
  where: {
    firstName: "Jane"
  }
});
```
- ##### Delete in bulk
  ```js
  const remove = await bulkDelete(records: Array, options: object): Promise<Array<Model>>
  ```
### Ordering Results
- The `order` option takes an array of items to order the query by or a sequelize method.
  - These items are themselves arrays in the form `[column, direction]`.
  - The column will be escaped correctly and the direction will be checked in a whitelist of valid directions (such as `ASC`, `DESC`, `NULLS FIRST`, etc).
```js
Model.findAll({
  order: [
    // Will escape name and validate DESC | ASC against a list of valid direction parameters
    ['name', 'DESC' | 'ASC']
  ]
})
```
```js
Model.findOne({
  order: [
    // will return `name` DESC or ASC
    ['name', `DESC` | `ASC`],
    // will return max('age')
    sequelize.fn('max', sequelize.col('age')),
    // will return max('age') DESC
    [sequelize.fn('max', sequelize.col('age')), 'DESC'],
  ]
});
```
The elements of the order array can be the following:
- A string (which will be automatically quoted)
- An array, whose first element will be quoted, second will be appended verbatim
- An object with a `raw` field:
  - The content of `raw` will be added verbatim without quoting
  - Everything else is ignored, and if `raw` is not set, the query will fail
- A call to `Sequelize.fn` (which will generate a function call in SQL)
- A call to `Sequelize.col` (which will quote the column name)
#### Limits and Offset
- The `limit` and `offset` options allow you to work with limiting / pagination:
```js
// Fetch 10 instances/rows
Project.findAll({ limit: 10 });

// Skip 8 instances/rows
Project.findAll({ offset: 8 });

// Skip 5 instances and fetch the 5 after that
Project.findAll({ offset: 5, limit: 5 });
```
#### Grouping Results
- The syntax for grouping and ordering are equal, except that grouping does not accept a direction as last argument of the array (there is no `ASC`, `DESC`, `NULLS FIRST`, etc).
```js
Model.findAll({
  group: 'name'
});
// yields 'GROUP BY name'
```

##### Public Methods

| Action                                                  | Method                                                                                                                                                         |
|---------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Add a new column to a table                             | `async addColumn(table: string, key: string, attribute: object, options: object): Promise`                                                                     |
| Add a constraint to a table                             | `async addConstraint(tableName: string, options: object): Promise`                                                                                             |
| Add an index to a column                                | `async addIndex(tableName: string \| object, attributes: Array, options: object, rawTablename: string): Promise`                                               |
| Delete multiple records from a table                    | `async bulkDelete(tableName: string, where: object, options: object, model: Model): Promise`                                                                   |
| Insert multiple records into a table                    | `async bulkInsert(tableName: string, records: Array, options: object, attributes: object): Promise`                                                            |
| Update multiple records of a table                      | `async bulkUpdate(tableName: string, values: object, identifier: object, options: object, attributes: object): Promise`                                        |
| Change a column definition                              | `async changeColumn(tableName: string, attributeName: string, dataTypeOrOptions: object, options: object): *`                                                  |
| Create a database                                       | `async createDatabase(database: string, options: object): Promise`                                                                                             |
| Create an SQL function                                  | `async createFunction(functionName: string, params: Array, returnType: string, language: string, body: string, optionsArray: Array, options: object): Promise` |
| Create a schema                                         | `async createSchema(schema: string, options: object): Promise`                                                                                                 |
| Create a table with given set of attributes             | `async createTable(tableName: string, attributes: object, options: object, model: Model): Promise`                                                             |
| Describe a table structure                              | `async describeTable(tableName: string, options: object): Promise<object>`                                                                                     |
| Drop all schemas                                        | `async dropAllSchemas(options: object): Promise`                                                                                                               |
| Drop all tables from database                           | `async dropAllTables(options: object): Promise`                                                                                                                |
| Drop a database                                         | `async dropDatabase(database: string, options: object): Promise`                                                                                               |
| Drop an SQL function                                    | `async dropFunction(functionName: string, params: Array, options: object): Promise`                                                                            |
| Drop a schema                                           | `async dropSchema(schema: string, options: object): Promise`                                                                                                   |
| Drop a table from database                              | `async dropTable(tableName: string, options: object): Promise`                                                                                                 |
| Get foreign key references details for the table        | `async getForeignKeyReferencesForTable(tableName: string, options: object): *`                                                                                 |
| Returns all foreign key constraints of requested tables | `async getForeignKeysForTables(tableNames: string[], options: object): Promise`                                                                                |
| Remove a column from a table                            | `async removeColumn(tableName: string, attributeName: string, options: object): *`                                                                             |
| Remove a constraint from a table                        | `async removeConstraint(tableName: string, constraintName: string, options: object): *`                                                                        |
| Remove an already existing index from a table           | `async removeIndex(tableName: string, indexNameOrAttributes: string \| string[], options: object): Promise`                                                    |
| Rename a column                                         | `async renameColumn(tableName: string, attrNameBefore: string, attrNameAfter: string, options: object): Promise`                                               |
| Rename an SQL function                                  | `async renameFunction(oldFunctionName: string, params: Array, newFunctionName: string, options: object): Promise`                                              |
| Rename a table                                          | `async renameTable(before: string, after: string, options: object): Promise`                                                                                   |
| Show all schemas                                        | `async showAllSchemas(options: object): Promise<Array>`                                                                                                        |
| Upsert                                                  | `async upsert(tableName: string, insertValues: object, updateValues: object, where: object, options: object): Promise<boolean, ?number>`                       |

### Utility Methods
#### Count
- The `count` method simply counts the occurrences of elements in the database.
```js
console.log(`There are ${await Project.count()} projects`);

const amount = await Project.count({
  where: {
    id: {
      [Op.gt]: 25
    }
  }
});
console.log(`There are ${amount} projects with an id greater than 25`);
```
#### max, min, and sum
```js
await User.max('age'); // 40
await User.max('age', { where: { age: { [Op.lt]: 20 } } }); // 10
await User.min('age'); // 5
await User.min('age', { where: { age: { [Op.gt]: 5 } } }); // 10
await User.sum('age'); // 55
await User.sum('age', { where: { age: { [Op.gt]: 5 } } }); // 50
```

##### [Validations and Constraints](https://sequelize.org/master/manual/validations-and-constraints.html)
---
END
