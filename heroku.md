# Heroku for Rails App
__Rails 6.0.3.2_**

Deploy to heroku
----------------
-on progress-

Sqlite3 to PostgreSQL on pre-existing Rails App
-----------------------------------------------

1. open Gemfile
    - replace `gem 'sqlite3'`
    - to `gem 'pg'`

2. run `bundle install`

3. open `config/database.yml`
    - Remove
        ```
        default: &default
          adapter: sqlite3
          pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
          timeout: 5000

        development:
          <<: *default
          database: db/development.sqlite3

        # Warning: The database defined as "test" will be erased and
        # re-generated from your development database when you run "rake".
        # Do not set this db to the same as development or production.
        test:
          <<: *default
          database: db/test.sqlite3

        production:
          <<: *default
          database: db/production.sqlite3
        ```


    - Replace this:\
      **You will also need to change the** `database: to a custom name`
        ```
        default: &default
          adapter: postgresql
          pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
          timeout: 5000

        development:
          <<: *default
          database: your-app--tes_development

        # Warning: The database defined as "test" will be erased and
        # re-generated from your development database when you run "rake".
        # Do not set this db to the same as development or production.
        test:
          <<: *default
          database: your-app-test_test

        production:
          <<: *default
          database: your-app-test_production
        ```
  
  4. run `rails db:create db:migrate`
  
  5. run `git a . && gc -m 'change database from Sqlite3 to PostgreSQL`
  
  6. run `git push origin master`
  
     - if you get this error message:
     
         ```
         To github.com:your-github-name/your-repository-name.git
         ! [rejected]        master -> master (fetch first)
         error: failed to push some refs to 'git@github.com:your-github-name/your-repository-name.git'
         hint: Updates were rejected because the remote contains work that you do
         hint: not have locally. This is usually caused by another repository pushing
         hint: to the same ref. You may want to first integrate the remote changes
         hint: (e.g., 'git pull ...') before pushing again.
         hint: See the 'Note about fast-forwards' in 'git push --help' for details.
         ```
     - run `git pull origin master`
     - then `git push origin master`
     
   7. run `heroku addons:create heroku-postgresql`
   
   8. run `git push heroku master`
   
   9. run `heroku run rails db:migrate`
  
  
