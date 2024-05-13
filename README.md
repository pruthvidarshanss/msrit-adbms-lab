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