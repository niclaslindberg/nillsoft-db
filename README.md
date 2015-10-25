# A simple Mysql PHP wrapper.
Main features of webx-db

* Name based auto-escaped parametrization.
* Hierarchical transactions by using `savepoint X` and `rollback to savepoint X` in inner transactions.
* Key violation exception with name of violated key.

## Getting started
```php
    use WebX\Db\Db;
    use WebX\Db\Impl\DbImpl;

    $db = new DbImpl([
        "user" => "mysqlUser",
        "password" => "mysqlPassword",
        "database" => "mysqlDatabase"
    ]);
```
### A simple insert
```php
    $values = ["firstName"=>"Alex", "lastName"=>"Morris"];
    $db->execute("INSERT INTO people (firstName,lastName) VALUES(:firstname,:lastName)", $values);

    $id = $db->insertId();          //The value of the autogenerated primary key.
```

### A simple select
```php
    foreach($db->allRows("SELECT * FROM table") as $row) {
        echo($row['firstName']);
        echo($row['lastName']);
    }
```

## How to run tests
In the root of the project:

  `composer install`

  `phpunit -c tests`

