# [`Program 1`](p1.md)

Draw ER/EER diagram for the library service requirement.

# [`Program 2`](p2.md)

Draw ER/EER diagram for the record company requirement.

# [`Program 3`](p3.md)

Draw ER diagram for the Movies information and execute SQL queries.

# [`Program 4`](p4.md)

Result for COMPANY database queries.

# `Question Bank Programs`

# [`Program 1`](qbp1.md)

[A] Suppose a movie_studio has several film crews. The crews might be designated by a given studio as crew1, crew 2, and so on. However, other studios might use the same designations for crews, so the attribute crew_number is not a key for crews. Movie_studio holds the information like name, branch and several locations. Each crew holds information like sector and strength.

* List all movie studios which are not used a single crews.
* Retrieve the movie studio which uses highest strength crew.
* Write a before insert trigger to check maximum number of crews to any studio is limited to 10.

[B] Consider the following restaurant database with the following attributes - Name, address – (building, street, area, pincode), id, cuisine, nearby landmarks, online delivery- yes/no, famous for (name of the dish). Create 10 collections with data relevant to the following questions. Write and execute MongoDB queries:

* List the name and address of all restaurants in Bangalore with Italian cuisine.
* List the name, address and nearby landmarks of all restaurants in Bangalore where north Indianthali is available.


# [`Program 2`](qbp2.md)

[A] The production company is organized into different studios. We store each studio’s name branch and location; every studio must own at least one movie. We store each movie’s title, sensor_number and year of production. Star may act in any number of movies and we store each actors name and address.

* List all the studios of the movie “Kantara”
* List all the actors , acted in a movie ‘Kantara’
* Write a deletion trigger, does not allow to deleting current year movies

[B] Consider the following restaurant table with the following attributes - Name, address –(building, street, area, pincode), id, cuisine, nearby landmarks, online delivery- (yes/no), famousfor(name of the dish) Create 10 collections with data relevant to the following questions. Write and execute MongoDB queries:

* List the name, address and nearby landmarks of all restaurants in Bangalore where north Indian thali is available
* List the name and address of restaurants and also the dish the restaurant is famous for, in Bangalore.


# [`Program 3`](qbp3.md)

[A] The production company is organized into different studios. We store each studio’s name branch and location; a studio own any number of Cartoon-serials. We store each Cartoon-Serial’s title, sensor_number and year of production. Star may do voices in any number of Cartoon-Serials and we store each actors name and address. 

* Find total no of actors, do voiced in a Cartoon-Serials ‘Tom and Jerry’
* Retrieve name of studio, location and Cartoon-Serials title in which star “Richard Kind” is voiced.
* Write a deletion trigger, does not allow to deleting current year Cartoon-Serials.

[B] Consider the following restaurant table with the following attributes - Name, address –(building, street, area, pincode), id, cuisine, nearby landmarks, online delivery-(yes/no), famous for(name of the dish) Create 10 collections with data relevant to the following questions. Write and execute MongoDB queries:

* List the name, address and nearby landmarks of all restaurants in Bangalore where north Indian thali is available.
* List the name and address of restaurants and also the dish the restaurant is famous for, in Bangalore where online delivery is available.


# [`Program 4`](qbp4.md)

[A] Car marketing company wants keep track of marketed cars and their owner. Each car must be associated with a single owner and owner may have any number of cars. We store car’s registration number, model & color and owner’s name, address & SSN. We also store date of purchase of each car.

* Find a person who owns highest number of cars
* Retrieve persons and cars information purchased on the day 03-03-2023
* Write a insertion trigger to check date of purchase must be less than current date (must use system date)


[B] Consider the following Tourist places table with the following attributes - Place, address – (state), id, tourist attractions, best time of the year to visit, modes of transport(include nearest airport, railway station etc), accommodation, food - what not to miss for sure Create 10 collections with data relevant to the following questions. Write and execute MongoDB queries:

* List all the tourist places of Karnataka
* List the tourist attractions of Kerala. Exclude accommodation and food


# [`Program 5`](qbp5.md)

[A] Puppy pet shop wants to keep track of dogs and their owners. The person can buy maximum three pet dogs. We store person’s name, SSN and address and dog’s name, date of purchase and sex. The owner of the pet dogs will be identified by SSN since the dog’s names are not distinct.

* List all pets owned by a person ‘Ramesh’.
* List all persons who are not owned a single pet
* Write a trigger to check the constraint that the person can buy maximum three pet dogs


[B] Consider the following Tourist places table with the following attributes - Place, address –(state, id), tourist attractions,best time of the year to visit,modes of transport(include nearest airport, railway station etc), accommodation, food - what not to miss for sureCreate 10 collections with data relevant to the following questions. Write and execute MongoDB queries:

* List the tourist attractions of Kerala. Exclude accommodation and food.
* List the places sorted state wise


# [`Program 6`]()

[A] Education institute is managing the on line course enrollment system. Students can enroll maximum of six courses of their choice and a maximum student to be enrolled to any course is 60. We store student details like name, USN, semester and several addresses, course details like unique title, unique id and credits.

* Find number of students enrolled for the course ‘ADBMS’
* Retrieve student names that are enrolled for AI course but not enrolled for IOT.
* Write a trigger to establish the constraint that the students can enroll maximum of six courses of their choice.


[B] Consider the following Tourist places table with the following attributes - Place, address – (state, id), tourist attractions,best time of the year to visit,modes of transport(include nearest airport, railway station etc), accommodation, food - what not to miss for sure Create 10 collections with data relevant to the following questions. Write and execute MongoDB queries:

* List all the tourist places of Karnataka
* List the places sorted state wise


# [`Program 7`]()

[A] The Sapna Book shop wants keep track of orders of the book. The book is composed of unique id, title, year of publication, single author and single publisher. Each order will be uniquely identified by order-id and may have any number of books. We keep track of quantity of each book ordered. We store the following details for author and publisher.
    a. AUTHOR: unique author-id, name, city, country
    b. PUBLISHER: unique publisher-id, name, city, country.

* Find the author who has published highest number of books
* List the books published by specific publisher during the year 2022.
* Write before insertion trigger to book to check year of publication should allow current year only.


[B] Consider the following Movie table with the following attributes Actor_name, Actor_id, Actor_birthdate, Dirctor_name,Director_id, Director_birthdate, film_title, year of production ,type (thriller, comedy, etc.) Create 10 collections with data relevant
to the following questions. Write and execute MongoDB queries:

* List all the movies acted by John in the year 2018
* List only the actors names and type of the movie directed by Ram


# [`Program 8`]()

[A] The commercial bank wants keep track of the customer’s account information. The each customer may have any number of accounts and account can be shared by any number of customers. The system will keep track of the date of last transaction. We store the following details.
    a. Account: unique account-number, type and balance
    b. Customer: unique customer-id, name and several addresses composed of street, city and state

* Add 3% interest to the customer who have less than 1000 balances and 6% interest to remaining customers.
* List joint accounts involving more than three customers
* Write a insertion trigger to allow only current date for date of last transaction field.


[B] Consider the following Movie table with the following attributes - Actor_name,Actor_id, Actor_birthdate , Dirctor_name,Director_id, Director_birthdate, film_title, year of production ,type (thriller, comedy, etc.) Create 10 collections with data relevant to the following questions. Write and execute MongoDB queries:

* List all the movies acted by John and Elly in the year 2012.
* List only the name and type of the movie where Ram has acted sorted by movie names


# [`Program 9`]()

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

* List all the movies acted by John and Elly in the year 2012.
* List only the name and type of the movie where Ram has acted, sorted by movie names.


# [`Program 10`]()

[A] Consider an ONLINE_AUCTION database system in which members (buyers and sellers) participate in the sale of items. The data requirements for this system are summarized as follows: Design an Enhanced Entity-Relationship diagram for the ONLINE_AUCTION database and build the design using a data modeling tool such as ERwin ,Rational Rose or erdplus.

* The online site has members, each of whom is identified by a unique member number and is described by an e-mail address, name, password, home address, and phone number.
* A member may be a buyer or a seller. A buyer has a shipping address recorded in the database. A seller has a bank account number and routing number recorded in the database.
* Items are placed by a seller for sale and are identified by a unique item number assigned by the system. Items are also described by an item title, a description, starting bid price, bidding increment, the start date of the auction, and the end date of the auction.
* Items are also categorized based on a fixed classification hierarchy (for example, a modem may be classified as COMPUTER→HARDWARE →MODEM).
* Buyers make bids for items they are interested in. Bid price and time of bid is recorded. The bidder at the end of the auction with the highest bid price is declared the winner and a transaction between buyer and seller may then proceed.
* The buyer and seller may record feedback regarding their completed transactions. Feedback contains a rating of the other party participating in the transaction (1–10) and a comment.


[B] Consider the following Movie table with the following attributes - Actor_name,Actor_id, Actor_birthdate , Dirctor_name,Director_id, Director_birthdate, film_title, year of production ,type (thriller, comedy, etc.) Create 10 collections with data relevant to the following questions. Write and execute MongoDB queries:

* List all the movies acted by John in the year 2018
* List only the actors names and type of the movie directed by Ram