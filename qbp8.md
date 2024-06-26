# `QB Program 8`

[A] The commercial bank wants keep track of the customer’s account information. The each customer may have any number of accounts and account can be shared by any number of customers. The system will keep track of the date of last transaction. We store the following details.
    a. Account: unique account-number, type and balance
    b. Customer: unique customer-id, name and several addresses composed of street, city and state

```SQL
CREATE TABLE ACCOUNTS (
    ACCOUNT_NO VARCHAR(20) PRIMARY KEY,
    TYPE VARCHAR(255),
    BALANCE DECIMAL(10, 2),
    LAST_TRANSACTION_DATE DATE
);

INSERT INTO ACCOUNTS (ACCOUNT_NO, TYPE, BALANCE, LAST_TRANSACTION_DATE) VALUES
('A01', 'Savings', 1500.00, '2024-05-06'),
('A02', 'Checking', 800.00, '2024-05-09'),
('A03', 'Savings', 1200.00, '2024-05-13');


CREATE TABLE CUSTOMERS (
    CUSTOMER_ID VARCHAR(20) PRIMARY KEY,
    NAME VARCHAR(255)
);

INSERT INTO CUSTOMERS (CUSTOMER_ID, NAME) VALUES
('C01', 'John Doe'),
('C02', 'Jane Smith'),
('C03', 'Alice Johnson'),
('C04', 'Johnny'),
('C05', 'Diana'),
('C06', 'Marcus'),
('C07', 'Spearow');

CREATE TABLE ADDRESSES (
    ADDRESS_ID INT AUTO_INCREMENT PRIMARY KEY,
    CUSTOMER_ID VARCHAR(20),
    STREET VARCHAR(255),
    CITY VARCHAR(255),
    STATE VARCHAR(255),
    FOREIGN KEY (CUSTOMER_ID) REFERENCES CUSTOMERS(CUSTOMER_ID)
);

INSERT INTO ADDRESSES (CUSTOMER_ID, STREET, CITY, STATE) VALUES
('C01', '123 Main St', 'Bengaluru', 'Karnataka'),
('C02', '456 Elm St', 'Kunigal', 'Goa'),
('C03', '5th Cross', 'Dharwad', 'Karnataka'),
('C04', '9th Main B', 'Gubbi', 'Karnataka'),
('C05', '1st Cross A', 'Kudure Mukha', 'Karnataka'),
('C06', '8th Cross', 'Hoysala', 'Karnataka'),
('C07', '4th Main', 'Gandhinagar', 'Karnataka');


CREATE TABLE JOINT_ACCOUNTS (
    ACCOUNT_NO VARCHAR(20),
    CUSTOMER_ID VARCHAR(20),
    FOREIGN KEY (ACCOUNT_NO) REFERENCES ACCOUNTS(ACCOUNT_NO),
    FOREIGN KEY (CUSTOMER_ID) REFERENCES CUSTOMERS(CUSTOMER_ID),
    PRIMARY KEY (ACCOUNT_NO, CUSTOMER_ID)
);

INSERT INTO JOINT_ACCOUNTS (ACCOUNT_NO, CUSTOMER_ID) VALUES
('A01', 'C01'),
('A01', 'C02'),
('A01', 'C03'),
('A02', 'C04'),
('A02', 'C05'),
('A02', 'C06'),
('A02', 'C07'),
('A02', 'C02');
```

* Add 3% interest to the customer who have less than 1000 balances and 6% interest to remaining customers.
```SQL
UPDATE ACCOUNTS
SET BALANCE = CASE 
                WHEN BALANCE < 1000 THEN BALANCE * 1.03
                ELSE BALANCE * 1.06
             END;
```

|ACCOUNT_NO|TYPE|BALANCE|LAST_TRANSACTION_DATE|
|---|---|---|---|
|A01|Savings|1590.00|2024-05-06|
|A02|Checking|824.00|2024-05-09|
|A03|Savings|1272.00|2024-05-13|


* List joint accounts involving more than three customers
```SQL
SELECT ACCOUNT_NO, COUNT(*) AS NUM_CUSTOMERS
FROM JOINT_ACCOUNTS
GROUP BY ACCOUNT_NO
HAVING NUM_CUSTOMERS > 3;
```

|ACCOUNT_NO|NUM_CUSTOMERS|
|---|---|
|A02|5|


* Write a insertion trigger to allow only current date for date of last transaction field.
```SQL
DELIMITER //

CREATE TRIGGER date_check
BEFORE INSERT ON ACCOUNTS
FOR EACH ROW
BEGIN
    IF NEW.LAST_TRANSACTION_DATE IS NOT NULL AND NEW.LAST_TRANSACTION_DATE != CURDATE() THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Invalid date for last transaction. Please use current date.';
    END IF;
END;
//

DELIMITER ;
```

```SQL
CREATE TRIGGER date_check BEFORE INSERT ON ACCOUNTS FOR EACH ROW BEGIN IF NEW.LAST_TRANSACTION_DATE IS NOT NULL AND NEW.LAST_TRANSACTION_DATE != CURDATE() THEN SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Invalid date for last transaction. Please use current date.'; END IF; END;;
```

```SQL
// Test Query
INSERT INTO ACCOUNTS (ACCOUNT_NO, TYPE, BALANCE, LAST_TRANSACTION_DATE) VALUES
('A04', 'Savings', 300.00, '2023-04-06');
```


[B] Consider the following Movie table with the following attributes - Actor_name,Actor_id, Actor_birthdate , Dirctor_name,Director_id, Director_birthdate, film_title, year of production ,type (thriller, comedy, etc.) Create 10 collections with data relevant to the following questions. Write and execute MongoDB queries:

```js
db.movies.insertMany([
  {
    Actor_name: "John",
    Actor_id: 1,
    Actor_birthdate: "1990-05-15",
    Director_name: "Mike",
    Director_id: 101,
    Director_birthdate: "1980-03-20",
    film_title: "Fast & Furious",
    year_of_production: 2018,
    type: "Action"
  },
  {
    Actor_name: "Alice",
    Actor_id: 2,
    Actor_birthdate: "1985-07-25",
    Director_name: "Jackson",
    Director_id: 102,
    Director_birthdate: "1975-11-10",
    film_title: "Beauty & the Beast",
    year_of_production: 2018,
    type: "Thriller"
  },
  {
    Actor_name: "Elly",
    Actor_id: 3,
    Actor_birthdate: "1992-01-02",
    Director_name: "Harry",
    Director_id: 103,
    Director_birthdate: "1978-09-16",
    film_title: "Drunken Monkey",
    year_of_production: 2012,
    type: "Comedy"
  },
  {
    Actor_name: "Mary",
    Actor_id: 4,
    Actor_birthdate: "1991-06-07",
    Director_name: "Cody",
    Director_id: 104,
    Director_birthdate: "1972-08-09",
    film_title: "Horror Story",
    year_of_production: 2018,
    type: "Horror"
  },
  {
    Actor_name: "Jameson",
    Actor_id: 5,
    Actor_birthdate: "1990-06-06",
    Director_name: "Paul",
    Director_id: 105,
    Director_birthdate: "1977-07-17",
    film_title: "Unstoppable",
    year_of_production: 2018,
    type: "Action"
  },
  {
    Actor_name: "Kofi",
    Actor_id: 6,
    Actor_birthdate: "1983-08-20",
    Director_name: "Hendrickson",
    Director_id: 106,
    Director_birthdate: "1979-04-08",
    film_title: "Animal Kingdom",
    year_of_production: 2016,
    type: "Comedy"
  },
  {
    Actor_name: "Allison",
    Actor_id: 7,
    Actor_birthdate: "1980-02-16",
    Director_name: "Lily",
    Director_id: 107,
    Director_birthdate: "1983-12-10",
    film_title: "Missing",
    year_of_production: 2019,
    type: "Thriller"
  },
  {
    Actor_name: "Roman",
    Actor_id: 8,
    Actor_birthdate: "1984-01-24",
    Director_name: "Sam",
    Director_id: 108,
    Director_birthdate: "1976-08-08",
    film_title: "Hidden Treasure",
    year_of_production: 2020,
    type: "Mystery"
  },
  {
    Actor_name: "Gunther",
    Actor_id: 9,
    Actor_birthdate: "1979-09-05",
    Director_name: "Austin",
    Director_id: 109,
    Director_birthdate: "1972-07-12",
    film_title: "Sacred",
    year_of_production: 2016,
    type: "Thriller"
  },
  {
    Actor_name: "Nancy",
    Actor_id: 10,
    Actor_birthdate: "1988-07-15",
    Director_name: "Eddy",
    Director_id: 110,
    Director_birthdate: "1976-08-02",
    film_title: "Exorcism",
    year_of_production: 2018,
    type: "Horror"
  },
  {
    Actor_name: "Rajamouli",
    Actor_id: 11,
    Actor_birthdate: "1984-05-19",
    Director_name: "Ram",
    Director_id: 111,
    Director_birthdate: "1972-02-14",
    film_title: "RRR",
    year_of_production: 2018,
    type: "Horror"
  },
  {
    Actor_name: "Ram", 
    Actor_id: 12, 
    Actor_birthdate: "1986-04-07", 
    Director_name: "Vikram", 
    Director_id: 112, 
    Director_birthdate: "1974-12-12", 
    film_title: "Yevadu", 
    year_of_production: 2016, 
    type: "Action"
  }
]);
```

* List all the movies acted by John and Elly in the year 2012.
```js
db.movies.aggregate([
  { $match: { Actor_name: { $in: ["John", "Elly"] }, year_of_production: 2012 } }
]);
```

```
[
  {
    _id: ObjectId('664372617209cd00749f9916'),
    Actor_name: 'Elly',
    Actor_id: 3,
    Actor_birthdate: '1992-01-02',
    Director_name: 'Harry',
    Director_id: 103,
    Director_birthdate: '1978-09-16',
    film_title: 'Drunken Monkey',
    year_of_production: 2012,
    type: 'Comedy'
  }
]
```

* List only the name and type of the movie where Ram has acted sorted by movie names
```js
db.collection1.find({ Actor_name: "Ram" }, { film_title: 1, type: 1, _id: 0 }).sort({ film_title: 1 });
```

```
[ { film_title: 'Yevadu', type: 'Action' } ]
```