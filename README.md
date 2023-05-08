# Cinema-App

The "Cinema-App" project is a user-friendly software application for streamlined movie ticket reservations. Users can create a basket, add tickets, and view their order history, while administrators can create movies, cinema halls, and sessions, and search for users by email. The program is easy-to-use and offers comprehensive functionality.

The database already has an injection:
- ADMIN: admin@gmail.com : 1234
- USER: user@gmail.com : 1234

## Features
- Register a new user
- Login (username and password)
- Role-based authorization (admin, user)
- Exception handling (invalid username, password, invalid role) with descriptive messages
- Project has multiple endpoints with user and admin access
    - POST: `/register` (to create a user) - `ALL`
    - POST: `/cinema-halls` (to create a cinema hall) - `ADMIN`
    - POST: `/movies` (to create a movie) - `ADMIN`
    - POST: `/movie-sessions` (to create a movie session) - `ADMIN`
    - POST: `/orders/complete` (to create an order for the current user) - `USER`
    - PUT: `/movie-sessions/{id}` (to update a movie session) - `ADMIN`
    - PUT: `/shopping-carts/movie-sessions` (to add movie session to the shopping cart) - `USER`
    - DELETE: `/movie-sessions/{id}` (to delete a movie session) - `ADMIN`
    - GET: `/orders` (to get order history for the current user) - `USER`
    - GET: `/shopping-carts/by-user` (to get a shopping cart for the current user) - `USER`
    - GET: `/cinema-halls` (to get all cinema halls) - `USER` or `ADMIN`
    - GET: `/movies` (to get all movies) - `USER` or `ADMIN`
    - GET: `/movie-sessions/available` (to get all available movies by date) - `USER` or `ADMIN`
    - GET: `/users/by-email` (to find user by email) - `ADMIN`

## Structure
#### The package structure of the project includes:
- `config`: This package contains Spring configuration files that define the application context and provide configuration for various beans.
- `controller`: This package contains the controllers for the different endpoints of the REST API. These controllers receive requests from clients, perform any necessary business logic, and send responses back to clients.
- `dao`: This package contains the data access layer (also known as the repository layer) that is responsible for accessing and manipulating data in the database.
- `dto`: This package contains data transfer objects that are used to encapsulate and transfer data between the different layers of the application. These objects help to unify requests and responses in the controllers.
- `exception`: This package contains the custom exception `DataProcessingException`.
- `lib`: This package contains email and password validators with their annotations. These validators help to ensure that the data provided by the user is valid and meets the requirements of the application.
- `model`: This package contains the models for the database. These models are used to represent data entities in the database and are used by the DAO to map database records to Java objects.
- `security`: This package contains `CustomUserDetailsService` that implements the UserDetailsService interface. The CustomUserDetailsService class is used to find a user by their email and transform the user object into a UserDetails object, which is used by Spring Security for authentication and authorization.
- `service`: This package contains the services that call the repositories and the `AuthenticationService` class. These services are responsible for performing business logic and coordinating the interactions between the controllers and the DAO.
  - `mapper`: This package contains mapper classes that convert model objects to DTO objects. These mappers are used to convert between dto and model (and are not used for DB communication)
- `util`: This package contains a utility class for date and time formatting.

## Security
The project has a built-in security mechanism that ensures the protection of user confidential information and ride data. To use the service, you need to register and authorize.
- Registration. To register for the service, you need to make a POST request to the following endpoint: POST `/register` Where registration is the endpoint that handles registration requests. The request body should contain the following fields:
  - login: user's email address
  - password: password for logging into the system
  - repeatPassword: uses to confirm the password
- Authorization. To authorize, make a POST request to the following endpoint: POST `/login` Where login is the endpoint that handles authorization requests. The request body should contain the following fields:
  - login: user's login address
  - password: password for logging into the system. Also, we can perform a logout (GET `/logout`).

## Technologies
- Java 17
- Apache Maven
- Apache Tomcat - version 9.0.73
- MySQL
- Hibernate
- Spring:
    - Core
    - Web Mvc
    - Security

## How to Run and Test
To run the project locally, follow these steps:
- Clone the project
- Modify the `db.properties` file located in `resources/db.properties`
- Build the project using Maven: `mvn package`
- Create a local Tomcat configuration in IntelliJ and run it to deploy the application. Once the application is up and running, you can access it at localhost:8080.

To test the application, you can use the mock admin and user accounts with the credentials 
- ADMIN (username: admin@gmail.com and password: 1234)
- USER (username: user@gmail.com and password: 1234).