# The 41 Against

A one-page site listing the 41 Australian senators who voted against marriage equality in September 2012, with their party, state, and contact details, so people could get in touch. It's a sister site to [The 98 Against](https://github.com/superhighfives/the-98-against), which covered the House of Representatives.

Status: archived. Made in 2012 and hosted on Heroku, not maintained. Australia legalized same-sex marriage in 2017.

## Running it

```sh
bundle
bundle exec rackup
```

The repo includes a SQLite database (`the41against.db`) with the data already loaded. To rebuild it:

```sh
bundle exec rake db:migrate
bundle exec rake "csv_model_import[db/the41against.csv,Politician]"
```

It pins Ruby 2.2.4 and old gems, so it needs an old Ruby to run.

## How it works

- `app.rb` is a Sinatra app that loads every `Politician` from the database and renders `views/index.haml`. It uses SQLite locally and Postgres (from `DATABASE_URL`) in production.
- `db/the41against.csv` holds the senators and their details, and the `Rakefile` imports it.
- Styles are Sass with Compass in `views/stylesheets/`.
