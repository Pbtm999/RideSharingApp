# RideSharingApp

A ride-sharing application developed as an academic project for the **Software Architecture** course of the BSc in Computer Science at FCUP.

The system matches nearby drivers and passengers travelling towards compatible destinations, allowing users to create rides, receive potential matches, select matching preferences and rate other users after completing a ride.

**Grade: 19/20**

## Architecture

The project was developed in two stages:

* **Core / Domain** — ride-sharing business logic, user management, ride matching, spatial indexing and persistence.
* **Web Application** — a Spring Boot and Vaadin interface built on top of the domain layer.

The project focuses on software architecture principles such as separation of concerns, interface-based abstractions and the use of design patterns.

## Main Features

* User registration and authentication
* Driver and passenger rides
* Location-based ride matching
* Matching based on proximity and compatible destinations
* User-defined match preferences
* Match acceptance
* Driver/passenger rating system
* Interactive map-based interface
* User persistence between executions

## Spatial Matching

Active rides are indexed using a **Point Quadtree**.

When a user's position is updated, the application queries the quadtree for nearby rides within a configurable radius and evaluates possible matches.

A valid match requires rides to:

* be sufficiently close to each other;
* have compatible destinations;
* have complementary roles — driver and passenger;
* not already be matched.

This avoids having to scan every active ride whenever a user's location changes.

## Design Patterns

Several design patterns were explored throughout the project.

### Facade

`Manager` exposes the main operations required by the application while hiding the internal user and matching subsystems.

`PointQuadtree` also provides a simplified interface over the underlying tree structure.

### Singleton

The application maintains shared instances of the main manager and user repository.

### Visitor

The quadtree implementation uses the Visitor pattern to perform operations over node and leaf elements while keeping traversal logic separated from the tree structure.

### Factory Method

Rides provide comparators used to order potential matches according to each user's preferred matching strategy.

## Matching Preferences

Users can prioritise different characteristics when potential rides are presented, such as:

* better-rated users;
* cheaper rides;
* closer rides.

Potential matches are ordered according to the active preference.

## Web Application

The user interface was implemented with:

* **Java**
* **Spring Boot**
* **Vaadin**
* **Google Maps integration**
* **Maven**

The Spring `ManagerService` acts as the bridge between the Vaadin views and the domain layer.

The application includes views for:

* login and registration;
* user information and preferences;
* ride creation and management;
* visual ride interaction using a map.

## Testing

The core domain implementation contains unit tests covering major components such as:

* users;
* rides;
* matching;
* locations;
* quadtrees;
* the application manager.

The web project also includes integration-test infrastructure using Vaadin TestBench.

## Technologies

`Java` · `Spring Boot` · `Vaadin` · `Maven` · `JUnit` · `Google Maps` · `Software Architecture` · `Design Patterns`

## Repositories

### Core / Domain

Contains the original implementation of the ride-sharing domain, matching system, quadtree and tests.

**Repository:** `Backend-Ride-Sharing-App`

### Web Application

Contains the Spring Boot + Vaadin application and integration with the domain layer.

**Repository:** `Frontend-Ride-Sharing-App`

## Running the Web Application

Requirements:

* Java 17 or newer
* Maven, or the included Maven Wrapper

Run:

```bash
./mvnw spring-boot:run
```

On Windows:

```powershell
mvnw.cmd spring-boot:run
```

The application will then be available at:

```text
http://localhost:8080
```

## Academic Context

Developed as a group academic project for the **Software Architecture** course of the **BSc in Computer Science at FCUP — University of Porto**.

**Final grade: 19/20**
