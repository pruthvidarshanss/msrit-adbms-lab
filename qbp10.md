# `QB Program 10`

[A] Consider an ONLINE_AUCTION database system in which members (buyers and sellers) participate in the sale of items. The data requirements for this system are summarized as follows: Design an Enhanced Entity-Relationship diagram for the ONLINE_AUCTION database and build the design using a data modeling tool such as ERwin ,Rational Rose or erdplus.

* The online site has members, each of whom is identified by a unique member number and is described by an e-mail address, name, password, home address, and phone number.
* A member may be a buyer or a seller. A buyer has a shipping address recorded in the database. A seller has a bank account number and routing number recorded in the database.
* Items are placed by a seller for sale and are identified by a unique item number assigned by the system. Items are also described by an item title, a description, starting bid price, bidding increment, the start date of the auction, and the end date of the auction.
* Items are also categorized based on a fixed classification hierarchy (for example, a modem may be classified as COMPUTER→HARDWARE →MODEM).
* Buyers make bids for items they are interested in. Bid price and time of bid is recorded. The bidder at the end of the auction with the highest bid price is declared the winner and a transaction between buyer and seller may then proceed.
* The buyer and seller may record feedback regarding their completed transactions. Feedback contains a rating of the other party participating in the transaction (1–10) and a comment.


[B] Consider the following Movie table with the following attributes - Actor_name,Actor_id, Actor_birthdate , Dirctor_name,Director_id, Director_birthdate, film_title, year of production, type (thriller, comedy, etc.) Create 10 collections with data relevant to the following questions. Write and execute MongoDB queries:

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