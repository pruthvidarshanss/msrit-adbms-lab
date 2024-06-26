# `QB Program 7`

[A] The Sapna Book shop wants keep track of orders of the book. The book is composed of unique id, title, year of publication, single author and single publisher. Each order will be uniquely identified by order-id and may have any number of books. We keep track of quantity of each book ordered. We store the following details for author and publisher.
    a. AUTHOR: unique author-id, name, city, country
    b. PUBLISHER: unique publisher-id, name, city, country.

```SQL
CREATE TABLE AUTHORS (
    AUTHOR_ID INT PRIMARY KEY,
    NAME VARCHAR(255),
    CITY VARCHAR(255),
    COUNTRY VARCHAR(255)
);

INSERT INTO AUTHORS (AUTHOR_ID, NAME, CITY, COUNTRY) VALUES
(101, 'Johnny', 'New York', 'USA'),
(102, 'Rocky', 'San Andreas', 'USA');


CREATE TABLE PUBLISHERS (
    PUBLISHER_ID INT PRIMARY KEY,
    NAME VARCHAR(255),
    CITY VARCHAR(255),
    COUNTRY VARCHAR(255)
);

INSERT INTO PUBLISHERS (PUBLISHER_ID, NAME, CITY, COUNTRY) VALUES
(201, 'Marvel', 'Chicago', 'USA'),
(202, 'DC', 'London', 'UK');


CREATE TABLE BOOKS (
    BOOK_ID INT PRIMARY KEY,
    TITLE VARCHAR(255),
    YEAR_OF_PUBLICATION INT,
    AUTHOR_ID INT,
    PUBLISHER_ID INT,
    FOREIGN KEY (AUTHOR_ID) REFERENCES AUTHORS(AUTHOR_ID),
    FOREIGN KEY (PUBLISHER_ID) REFERENCES PUBLISHERS(PUBLISHER_ID)
);

INSERT INTO BOOKS (BOOK_ID, TITLE, YEAR_OF_PUBLICATION, AUTHOR_ID, PUBLISHER_ID) VALUES
(301, 'Damage', 2022, 101, 201),
(302, 'Missing', 2023, 101, 201),
(303, 'Fate', 2022, 101, 201),
(304, 'Romantic', 2022, 102, 202),
(305, 'Raw', 2023, 102, 202),
(306, 'SmackDown', 2021, 101, 202),
(307, 'Friends', 2024, 102, 202);


CREATE TABLE ORDERS (
    ORDER_ID INT AUTO_INCREMENT PRIMARY KEY,
    BOOK_ID INT,
    QUANTITY INT,
    FOREIGN KEY (BOOK_ID) REFERENCES BOOKS(BOOK_ID)
);

INSERT INTO ORDERS (BOOK_ID, QUANTITY) VALUES
(301, 10),
(302, 5),
(303, 8),
(304, 3),
(305, 4),
(306, 9),
(307, 2);
```

* Find the author who has published highest number of books
```SQL
SELECT a.NAME AS AUTHOR_NAME, COUNT(b.BOOK_ID) AS BOOK_COUNT
FROM AUTHORS a
JOIN BOOKS b ON a.AUTHOR_ID = b.AUTHOR_ID
GROUP BY a.AUTHOR_ID
ORDER BY BOOK_COUNT DESC
LIMIT 1;
```

|AUTHOR_NAME|BOOK_COUNT|
|---|---|
|Johnny|4|

* List the books published by specific publisher during the year 2022.
```SQL
SELECT TITLE, YEAR_OF_PUBLICATION
FROM BOOKS
WHERE PUBLISHER_ID = (SELECT PUBLISHER_ID FROM PUBLISHERS WHERE NAME = 'Marvel')
AND YEAR_OF_PUBLICATION = 2022;
```

|TITLE|YEAR_OF_PUBLICATION|
|---|---|
|Damage|2022|
|Fate|2022|

* Write before insertion trigger to book to check year of publication should allow current year only.
```SQL
DELIMITER //

CREATE TRIGGER check_current_year_publication
BEFORE INSERT ON BOOKS
FOR EACH ROW
BEGIN
    DECLARE current_year INT;
    SET current_year = YEAR(CURDATE());
    IF NEW.YEAR_OF_PUBLICATION <> current_year THEN
        SIGNAL SQLSTATE '45000' 
        SET MESSAGE_TEXT = 'Year of publication should be of current year only.';
    END IF;
END;
//

DELIMITER ;
```

```SQL
CREATE TRIGGER check_current_year_publication BEFORE INSERT ON BOOKS FOR EACH ROW BEGIN DECLARE current_year INT; SET current_year = YEAR(CURDATE()); IF NEW.YEAR_OF_PUBLICATION <> current_year THEN SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Year of publication should be of current year only.'; END IF; END;;
```

```SQL
// Test query
INSERT INTO BOOKS (BOOK_ID, TITLE, YEAR_OF_PUBLICATION, AUTHOR_ID, PUBLISHER_ID) VALUES
(308, 'Cable', 2020, 102, 201);
```


[B] Consider the following Movie table with the following attributes Actor_name, Actor_id, Actor_birthdate, Dirctor_name,Director_id, Director_birthdate, film_title, year of production ,type (thriller, comedy, etc.) Create 10 collections with data relevant
to the following questions. Write and execute MongoDB queries:

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
  }
]);
```

* List all the movies acted by John in the year 2018
```js
db.movies.find({ Actor_name: "John", year_of_production: 2018 });
```

```
[
  {
    _id: ObjectId('664372617209cd00749f9914'),
    Actor_name: 'John',
    Actor_id: 1,
    Actor_birthdate: '1990-05-15',
    Director_name: 'Mike',
    Director_id: 101,
    Director_birthdate: '1980-03-20',
    film_title: 'Fast & Furious',
    year_of_production: 2018,
    type: 'Action'
  }
]
```

* List only the actors names and type of the movie directed by Ram
```js
db.movies.find({ Director_name: "Ram" }, { Actor_name: 1, type: 1, _id: 0 });
```

```
[ { Actor_name: 'Rajamouli', type: 'Horror' } ]
```