# Task
**Problem Statement:**
Design a Grocery Booking API:
Roles:
- Admin
- User

**Mandatory Requirements:**
**A. Design API endpoints**

1. Admin Responsibilities:
- Add new grocery items to the system
- View existing grocery items
- Remove grocery items from the system
- Update details (e.g., name, price) of existing grocery items
- Manage inventory levels of grocery items
2. User Responsibilities:
- View the list of available grocery items
- Ability to book multiple grocery items in a single order

**Advanced Challenge:**
- Docker: Containerize the application using Docker for ease of deployment and scaling.
- Database: Use any relational database of your choice.

Approach:

|           |   | API                                                                                                                    | Function                            | Input              | Output              | Logic (in Brief)                                                                                                    | Exception Cases                                        |
| --------- | - | ---------------------------------------------------------------------------------------------------------------------- | ----------------------------------- | ------------------ | ------------------- | ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------ |
| ADMIN API | 1 | [http://localhost:8091/admin/view](http://localhost:8091/admin/view)                                                   | View all grocery Items              | NONE               | List of DTO objects | fetch all the items from DB                                                                                         | Handle no objects present scenario                     |
| ADMIN API | 2 | [http://localhost:8091/admin/add](http://localhost:8091/admin/add)                                                     | Add an item in DB                   | DTO object         | DTO Item object     | map to an entity and store in DB                                                                                    | Validate the fields. Exception, incase of saving in DB |
| ADMIN API | 3 | [http://localhost:8091/admin/remove/1](http://localhost:8091/admin/remove/1)                                           | Deletes an item                     | id                 | String              | Deletes an item. (preferably also provide an option for soft delete)                                                | If the id doesnot exist                                |
| ADMIN API | 4 | [http://localhost:8091/admin/update/3](http://localhost:8091/admin/update/3)                                           | Updatesan item                      | id and DTO payload | Dto object          | updates the item                                                                                                    | if the ids donot match.                                |
| ADMIN API | 5 | [http://localhost:8091/admin/manageInventory/2?quantity=45](http://localhost:8091/admin/manageInventory/2?quantity=45) | Manage inventory                    | id and quantity    | DTO                 | update the quanity of the item                                                                                      | If the id is not present                               |
| USER API  | 6 | [http://localhost:8091/grocery/items](http://localhost:8091/grocery/items)                                             | Display all the items               |                    | List of DTO objects | Display only those items whose quantity are greater then 0                                                          | Handle no objects present scenario                     |
| USER API  | 7 | [http://localhost:8091/grocery/bookOrder](http://localhost:8091/grocery/bookOrder)                                     | Enables User to book multiple items | id List            | String              | Decrement the quantity of each item by 1. Prefer to create a table of users and orders and map them with the items. | Item ids are invalid                                   |


DB:
1. PostgreSQL (pgAdmin4)
2. Tables Structure

| Users Table               | Items Table       | Orders Table        | Order_Items_Mapping |
| ----------------- | ------------ | ------------ | ------------------- |
| user_id (PK)      | item_id (PK) | order_id(PK) | mapping_id (PK)     |
| Name              | name         | user_id      | order_id (FK)       |
| Role (ADMIN/USER) | price        |              | item_id (FK)        |
|                   | quanity      |              |                     |

Other cross-cutting concerns handled are:
1. Ensuring only Admin has access to Admin Controller, by extending the Security Configs.
2. Use of Collection Streams, wherever needed.
3. DTO Pattern implemented
4. Mapper used to map Entities to DTO, and vice versa.
5. Proper Exceptional Handling to gracefully catch exceptions and ensuring system doesn't abrupted shutdown.
6. Security, such as authenticated users (using user roles) are authorised.
7. Validation Checks added.
8. NPEs taken into mind.
9. Loggers added.
10. Ensured code follows the SonarLint standards.
11. Added Postman collections to assist in API testings.


Hoping this meets the criteria. Happy Evaluation! 

 
