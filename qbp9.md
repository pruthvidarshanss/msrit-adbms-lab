# `QB Program 9`

[A] Consider a database system for a baseball organization such as the major leagues. The data requirements are summarized as follows: Design an Enhanced Entity-Relationship diagram for the BASEBALL database. and build the design using a data modeling tool such as ERwin ,Rational Rose or erdplus. 

* The personnel involved in the league include players, coaches, managers, and umpires. Each is identified by a unique personnel id. They are also described by their first and last names along with the date and place of birth.
* Players are further described by other attributes such as their batting orientation (left, right, or switch) and have a lifetime batting average (BA).
* Within the players group is a subset of players called pitchers. Pitchers have a lifetime ERA (earned run average) associated with them.
* Teams are uniquely identified by their names. Teams are also described by the city in which they are located and the division and league in which they play (such as Central division of the American League).
* Teams have one manager, a number of coaches, and a number of players.
* Games are played between two teams with one designated as the home team and the other the visiting team on a particular date. The score (runs, hits, and errors) are recorded for each team. The team with the most runs is declared the winner of the game.
* With each finished game, a winning pitcher and a losing pitcher are recorded. In case there is a save awarded, the save pitcher is also recorded.
* With each finished game, the number of hits (singles, doubles, triples, and home runs) obtained by each player is also recorded


[B] Consider the following Movie table with the following attributes - Actor_name, Actor_id, Actor_birthdate, Director_name, Director_id, Director_birthdate, film_title, year of production, type (thriller, comedy, etc.) Create 10 collections with data relevant
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

* List only the name and type of the movie where Ram has acted, sorted by movie names.
```js
db.collection1.find({ Actor_name: "Ram" }, { film_title: 1, type: 1, _id: 0 }).sort({ film_title: 1 });
```

```
[ { film_title: 'Yevadu', type: 'Action' } ]
```