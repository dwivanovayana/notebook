# Heroku for Rails App
__Rails 6.0.3.2_**

Deploy to heroku
----------------

Sqlite3 to PostgreSQL on pre-existing Rails App
-----------------------------------------------

1. open Gemfile
...replace `gem 'sqlite3'`
...to `gem 'pg'`

2. run `bundle install`

3. open `config/database.yml`
