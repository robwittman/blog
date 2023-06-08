---
title: Setting up 
---

## Setup Rails app

I prefer to use the same database during development, so postgres
I want to try out TailwindCSS, so let's give it a go
```shell 
rails new orthus --database=postgresql --css=tailwind
```

## Setup dependencies

Let's setup docker-compose to use Postgres locally 
```yaml 
version: '3.1'

services:

  db:
    image: postgres
    ports:
      - 5432:5432
    volumes:
      - ./data/postgres:/var/lib/postgresql/data
    environment:
      POSTGRES_PASSWORD: password
```

`config/database.yaml`
```yaml 
default: &default
  adapter: postgresql
  encoding: unicode
  url: <%= ENV["DATABASE_URL"] %>
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>

development:
  <<: *default
  database: orthus_development

test:
  <<: *default
  database: orthus_test

production:
  <<: *default
  database: orthus_production
```

Setup our ENV file
``` 
DATABASE_URL=postgresql://postgres:password@127.0.0.1:5432/orthus_development
```

## Verify we can run the server 
```shell 
docker compose up -d
bin/dev 
```

If we open our browser at http://localhost:3000, we can load our application, and its connected to our database. Easy enough