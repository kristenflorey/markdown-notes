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
##### Create a Table
- Usually used in the `up()` method
```
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
```
return queryInterface.dropTable(<TableName>);
```

##### Adding a column
```
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
```
return queryInterface.removeColumn(<TableName>, <columnName>);
```
