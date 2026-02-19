# Photo Sharing App - DB Design

Let's design the database of a photo sharing app.

Q1. What type of things we are storing?
- users
- photo
- comments
- likes


Q2. What properties does each thing have?



Q3. What type of data does each property contains?


## Rough ER Diagram

```mermaid
graph TD
    subgraph DB ["Photo-Sharing App"]
        direction TB
        
        %% Nodes
        users[users]
        photos[photos]
        comments[comments]
        likes[likes]

        %% Horizontal spacing hack (forces users and photos to have distance)
        users ~~~ photos
        
        %% Vertical Relationships
        users --> photos
        users --> comments
        users --> likes
        
        photos --> comments
        photos --> likes

        %% Push the bottom row down to avoid line overlap
        photos ~~~ comments
        photos ~~~ likes
    end

    %% Styling
    style users fill:#ffe5cc,stroke:#d6b656
    style photos fill:#ffe5cc,stroke:#d6b656
    style comments fill:#ffe5cc,stroke:#d6b656
    style likes fill:#ffe5cc,stroke:#d6b656
    style DB fill:#d5e8d4,stroke:#82b366
```
 
## Relationships

1. Between user and photos: A user has many photos so this is a 1 to many relationship.
2. Between photos and user: looking from the perspective of photo, we have many to 1 relationship.
3. Between a photo and comments: 1 to many as a photo has many comments.
4. Between comments and a photo: many to 1.
5. Between a user and likes: 1 to many


## Misc
- Some other forms of relationship
- 1 to 1 example: a boat has a captain | a company has a CEO | a driver has a license
- Many to Many: tasks and engineers | a task can be worked by many engineers and one engineer can work on many tasks | students and classes, a student can attend many classes and a class has many students.
