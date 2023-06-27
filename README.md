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
1. Ensure that Ruby and Rails are installed on your system.
2. Open a terminal or command prompt and navigate to the desired directory where you want to create your Rails application.
3. Run the following command to create a new Rails application:
```
rails new receptionist-doctor-portal --database=postgresql
```
 👆 This command creates a new Rails application with PostgreSQL as the database.<br>
 
4. Navigate into the application directory:
```
cd receptionist-doctor-portal
```

### Step 2: Create the User model and authentication
1. Generate the User model and migration for authentication:
```
rails generate model User email:string password_digest:string role:string
```
👆This command generates a User model with email, password_digest, and role attributes.<br>

2. Run the migration to create the users table in the database:
```
rails db:migrate
```
3. Install the bcrypt gem for password encryption. Add it to the Gemfile:
```
gem 'bcrypt', '~> 3.1.7'
```
Then, run `bundle install` to install the gem.

4. Update the User model to include authentication logic. Add the following code to `app/models/user.rb`:
```
class User < ApplicationRecord
  has_secure_password
  validates :email, presence: true, uniqueness: true
  validates :role, presence: true

  # Additional code for role-based authorization (optional)
end
```
This code uses the `has_secure_password` method provided by bcrypt to handle password encryption and authentication.

### Step 3: Set up the login page and sessions controller
1. Generate a sessions controller to handle user authentication:
``` 
rails generate controller Sessions new create destroy
 ```
2. Update the routes (`config/routes.rb`) to include the login and logout routes:
``` 
Rails.application.routes.draw do
  get '/login', to: 'sessions#new'
  post '/login', to: 'sessions#create'
  delete '/logout', to: 'sessions#destroy'

  # Additional routes for other functionalities
end
 ```
3. Update the sessions controller (`app/controllers/sessions_controller.rb`) to handle authentication:
```
class SessionsController < ApplicationController
  def new
  end

  def create
    user = User.find_by(email: params[:session][:email].downcase)
    if user && user.authenticate(params[:session][:password])
      log_in(user)
      redirect_to root_url # Modify the redirection based on the user role
    else
      flash.now[:danger] = 'Invalid email/password combination'
      render 'new'
    end
  end

  def destroy
    log_out
    redirect_to root_url
  end
end
```
Here, `log_in` and `log_out` are helper methods that you need to define in `app/helpers/sessions_helper.rb`. These methods handle session management.

### Step 4: Create the Patient model and associated CRUD operations
1. Generate the Patient model and migration:
```
rails generate model Patient name:string age:integer
```
2. Run the migration to create the patients table in the database:
```
rails db:migrate
```
3. Update the Patient model (`app/models/patient.rb`) to include validations and associations:
```
class Patient < ApplicationRecord
  validates :name, presence: true
  validates :age, presence: true, numericality: { only_integer: true }

  # Additional code for associations with other models
end
```
4. Create the patient controller and views for CRUD operations:
```
rails generate controller Patients
```
👆This command generates the Patients controller and associated views.<br>

5. Update the routes to include the patient routes:
```
Rails.application.routes.draw do
  # ...

  resources :patients

  # ...
end
```

### Step 5: Implement additional functionalities and customize the views
- Modify the User model to include a role attribute and implement role-based authorization.
- Customize the login page and views for patients based on the user's role.
- Implement the graph functionality to represent patient registrations vs. days.

#### Remember to regularly migrate the database  (`rails db:migrate`)  after making changes to the models or running new migrations.

###### This is a basic outline to get you started with building the receptionist and doctor portals in a Ruby on Rails application. Feel free to customize and expand upon these steps based on your specific requirements and preferences.
