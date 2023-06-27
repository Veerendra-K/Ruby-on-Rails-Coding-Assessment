# Ruby-on-Rails-Coding-Assessment

## Description
<strong>Build a simple Rails application that consists of a receptionist portal and a doctor portal with the following tasks:</strong>
- A single login page for both portals.
- Receptionist can register a new patient and perform CRUD operations.
- Doctor can view registered patients and view a graph representing patient registrations vs. days.
  
## Expectations
- Good quality code
- Proper authentication implementation
- Creativity beyond the requirements

## Steps

### Step 1: Set up the Rails application
```
rails new receptionist-doctor-portal --database=postgresql
cd receptionist-doctor-portal
```
### Step 2: Create the User model and authentication
```
rails generate model User email:string password_digest:string role:string
rails db:migrate
```
- Install the bcrypt gem for password encryption.
- Update the User model to include authentication logic.
### Step 3: Set up the login page and sessions controller
``` 
rails generate controller Sessions new create destroy
 ```
- Update the routes to include login and logout routes.
- Update the sessions controller to handle authentication.
### Step 4: Create the Patient model and associated CRUD operations
```
rails generate model Patient name:string age:integer
rails db:migrate
```
- Update the Patient model to include validations and associations.
- Generate the patient controller and views for CRUD operations.
- Update the routes to include patient routes.
### Step 5: Implement additional functionalities and customize the views
- Modify the User model to include a role attribute and implement role-based authorization.
- Customize the login page and views for patients based on the user's role.
- Implement the graph functionality to represent patient registrations vs. days.
- Add any additional features or functionalities.

#### Remember to regularly migrate the database  (`rails db:migrate`)  after making changes to the models or running new migrations.

###### This is a basic outline to get you started with building the receptionist and doctor portals in a Ruby on Rails application. Feel free to customize and expand upon these steps based on your specific requirements and preferences.
