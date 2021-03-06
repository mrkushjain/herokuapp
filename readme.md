App Link - [ rails-heroku-app-by-kush.herokuapp.com ](http://rails-heroku-app-by-kush.herokuapp.com/)
# Setting Up Heroku Rails app

1. Install **ruby-1.9.3-p392** using rvm 
```
$ rvm install 1.9.3-p392 
$ rvm use 1.9.3-p392 --default
```

2. Install **postgreSQL 9.2.4**
```
$ brew install postgresql (on Mac)
```

3. Install bundler
    
    ```
    $ gem install bundler
    ```

4. Create an account on heroku
[Signup on Heroku](https://api.heroku.com/signup/devcenter)

5. Install Heroku toolbelt
[Heroku Toolbelt](https://toolbelt.heroku.com/)

6. Login to Heroku

    ```
    $ heroku login
    ```

    Enter your heroku email and password

7. Create a new rails app

    ```
    $ rails new myapp --database=postgresql
    $ cd myapp
    ```

8. Install bundler
    
    ```
    $ gem install bundler
    ```

9. Start the postgres server

    ```
    $ pg_ctl -D /usr/local/var/postgres -l /usr/local/var/postgres/server.log start
    ```

10. Execute the SQL script from the following location:
[db.sql](https://github.com/mrkushjain/herokuapp/blob/master/db.sql)

    ```
    $ psql -f db.sql
    ```

11. Open config/database.yml and modify 
    ```
    password
    ```
    with
    ```
    password: password1
    ```
    everywhere in the file. Then add the line
    ```
    host: localhost
    ```
    at the end of each group
   
12. Create database

    ```
    $ rake db:migrate
    $ rake db:setup
    ```

13. Add the gem rails_12factor in gemfile by adding the following line in it
    ```
    gem 'rails_12factor', group: :production
    ```

14. Specify ruby version in gemfile by adding the following line in it
    ```
    ruby "1.9.3"
    ```

15. Run bundle install

    ```
    $ bundle install
    ```
    
16. In config/application.rb set the following configuration
    ```
    config.assets.initialize_on_precompile = false
    ```

18. Store your app in git

    ```
    $ git init
    $ git add .
    $ git commit -m "init"
    ```

19. Create heroku app

    ```
    $ heroku create
    ```
    
20. Add your ssh keys to heroku

    ```
    $ heroku keys:add ~/.ssh/id_rsa.pub
    ```

21. Deploy your code to heroku

    ```
    $ git push heroku master
    ```

22. Ensure we have one dyno running the web process type

    ```
    $ heroku ps:scale web=1
    ```

23. To see your app on heroku 

    ```
    $ heroku open
    ```

24. To see your app locally

    ```
    $ bundle exec rails s
    ```

25. Open [ Github ](www.github.com) and login with your username and password
26. Create a new repository with the name herokuapp
27. To add your app to github

    ```
    $ git remote add github git@github.com:mrkushjain/herokuapp.git
    $ git push github master
    ```
   
# View your app info

* Get Heroku Info

    ```
    $ heroku info
    ```
* Get Remote info

    ```
    $ git remote -v
    ```

# Renaming the app

1. Go to heroku app dashboard on browser and click on settings next to the app
2. Enter a new name and click on save
3. On the terminal type

   ```
   $ git remote rm heroku
   $ heroku git:remote -a newname
   ```
   where newname is the app's new name
4. Your new app is now accessible at new-name-of-app.herokuapp.com

# Adding Tests

Adding rspec tests
==================

1. Add rspec rails in your gemfile
    ```
    group :development, :test do
      gem 'rspec-rails'
    end
    ```
2. Run bundle install

    ```
    $ bundle install
    ```

3. Go to your terminal and use the same ruby version as you had you used while compiling postgres

    ```
    $ rvm use ruby-1.9.3-p392
    ```

4. Initialize the spec/ directory

    ```
    $ rails generate rspec:install
    ```

5. Run Tests with

    ```
    $ bundle exec rake spec
    ```

Adding Factory Girl
===================

1. Add gem factory_girl_rails under development and test groups
    ```
    group :development, :test do
      gem 'rspec-rails'
      gem 'factory_girl_rails'
    end
    ```
2. Run bundle install

    ```
    $ bundle install
    ```

Adding Should matchers
=======================
1. Add gem shoulda matchers in your gem under test
    ```
    group :test do
      gem "shoulda-matchers"
    end

    ```

2. Run bundle install

    ```
    $ bundle install
    ```
