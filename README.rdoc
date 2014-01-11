#A Test-Driven C.R.U.D Application w/RESTful Routing

##Stack
- Ruby 2.0.0
- Rails 3.2.13
- Postgresql 9.3.1.0
- ... see the Gemfile & Gemfile.lock


###So... you want a guide to build a Test-Driven C.R.U.D application with RESTful routing?
###You've come to the right place...

---

###What is a Test-Driven C.R.U.D application with RESTful routing?

#C.R.U.D Application
- **C**reate
  - Create new entries
- **R**ead
  - Read existing entries
- **U**pdate
  - Update existing entries
- **D**elete
  - Delete existing entries


---


#Test-Driven Development
- An application has many parts
- Writing tests helps use keep all those parts working
  - Let's say our application has 3 parts
    - We work on part 1
    - We get part 1 working
    - We work on part 2
    - We get part 2 working
    - We work on part 3
    - We get part 3 working
    - Does part 2 still work?... What about part 1?


---

#RESTful Routing
- My routes are consistent with the database action completed

###Requests:
- A `GET` request - Show me something... and don't change any of the data
- A `POST` request - Change the data
- A `PUT` request - Change the data
- A `DELETE` request - Change the data

###Routes:
- `GET     '/objects'`          - Show me all the objects in the database
- `POST    '/objects'`          - Insert a new object into the database
- `GET     '/objects/new'`      - Show me a form for a new object
- `GET     '/objects/:id/edit'` - Show me a form to edit an existing object (found by id)
- `GET     '/objects/:id'`      - Show me one of the object (found by id)
- `PUT     '/objects/:id'`      - Update an existing object in the database (found by id)
- `DELETE  '/objects'`          - Destroy an existing object in the database (found by id)

---


###Preface:


##Help Me "Error" Messages!!!
- NO ONE knows all the steps
- "Error" messages are part of the documentation on how something works

###Where do I start?!
- Many tasks in development do NOT have a "correct" order 
- Programming is about compartmentalizing problems until each problem is wholely understandable and quickly completely
  - Do you know how to complete your programming task?
    - `YES` - Complete it
    - `NO`  - Break off a smaller sub-task
 
#Rails Generators
- Do NOT use a rails generators unless you have a COMPLETE understanding of EVERYTHING the specific generator does and are 100% confident you can complete ALL those tasks without the generator quickly
- Generators are for speedy productivity, **NOT** for removing the need to understand


---

#Ready?
#Set?
#GO!


---


###Create your application!!!
- `rails new testful_restful_crud` creates all the files and folders needed for a Rails application named testful_restful_crud
- `-d postgresql` includes the `pg` gem in the Gemfile and sets up the database.yml file with a postgresql configuration
- `-T` allows us to omit TestUnit in our application (I want to use RSPEC instead)


```ruby

rails new testful_restful_crud -d postgresql -T

```


---


###Set up your database!!!
- Remember how that `-d postgresql` flag set up... well that included using a postgresql username... which is probably not correct.  Edit the `config/database.yml` file to have the correct username... if your postgresql server requires it.  


####For example:

```yml

development:
  adapter: postgresql
  encoding: unicode
  database: testful_restful_crud_development
  pool: 5
  username: testful_restful_crud  # <- this is probably not correct... Change it to your username if needed.  (In this demo, I just remove the username and password because my system does not require it)
  password:

```

---


###Create your database!!
- We have configured our database... let's create it.
- Be sure your posgresql server is running!
- `rake db:create` will create the databases mentioned in your `database.yml` file



---

###Set up for TESTING!!!!
- Let's use RSPEC
- Put `gem 'rspec-rails'` in our Gemfile
  - You've touched the Gemfile... so you immediately `bundle install`
- Now that `rspec-rails` is available, run `rails generate rspec:install`
  - This sets up the `spec` directory in our project
  - In the `spec` director we now have a `spec_helper.rb`
  - From this point on, some of the rails generators will also create a `_spec.rb` file... for testing whatever was generated
- Let's use Capybara for view testing
- Put `gem 'capybara'` in our Gemfile
  - You've touched the Gemfile... so you immediately `bundle install`
- Edit the `spec_helper.rb` to `require capybara/rspec`


---


###Test-Driving Begins to create a one model C.R.U.D application
###Test-First!!!!

```bash

mkdir spec/models
touch spec/models/my_model_spec.rb

```

###Step 1: Write a failing tests ("Make it RED")
###Step 2: Make the test pass ("Make it GREEN")
###Step 3: Refactor (be sure same thing is being tested)
###Step 4: Return to `Step 1`

