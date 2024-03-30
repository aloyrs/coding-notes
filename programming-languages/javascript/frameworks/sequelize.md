# Using Sequelize with PostgreSQL in JavaScript

Sequelize is an Object-Relational Mapping (ORM) library for Node.js, providing a powerful and intuitive way to interact with relational databases by mapping JavaScript objects to database tables.

It simplifies database operations, supports multiple database systems, and enhances code readability and maintainability by abstracting away the complexities of SQL queries.

## Installation

Install Sequelize and the PostgreSQL driver using npm:

```bash
npm install sequelize pg
```

## Setup

1. **Import Sequelize:**

   ```javascript
   const { Sequelize } = require("sequelize");
   ```

2. **Create Sequelize Instance:**

   ```javascript
   const sequelize = new Sequelize({
     database: "your_database_name",
     username: "your_username",
     password: "your_password",
     host: "localhost",
     dialect: "postgres",
   });
   ```

## Define Models

3. **Define a Model:**

   ```javascript
   const User = sequelize.define("User", {
     // Define model attributes
     firstName: {
       type: Sequelize.STRING,
     },
     lastName: {
       type: Sequelize.STRING,
     },
     // ...
   });
   ```

4. **Sync Models with Database:**

   ```javascript
   // Synchronize models with the database
   sequelize.sync({ force: true }).then(() => {
     console.log("Database and tables synced!");
   });
   ```

## CRUD Operations

5. **Create a Record:**

   ```javascript
   const newUser = await User.create({ firstName: "John", lastName: "Doe" });
   ```

6. **Read Records:**

   ```javascript
   const allUsers = await User.findAll();
   ```

   ```javascript
   const specificUser = await User.findOne({ where: { firstName: "John" } });
   ```

7. **Update a Record:**

   ```javascript
   await User.update({ lastName: "Smith" }, { where: { firstName: "John" } });
   ```

8. **Delete a Record:**

   ```javascript
   await User.destroy({ where: { firstName: "John" } });
   ```

## Advanced Features

9. **Associations:**

   Define associations between models:

   ```javascript
   User.hasMany(Project);
   Project.belongsTo(User);
   ```

10. **Query with Conditions:**

    Use Sequelize operators for complex queries:

    ```javascript
    const Op = Sequelize.Op;

    const users = await User.findAll({
      where: {
        lastName: {
          [Op.like]: "D%",
        },
      },
    });
    ```
