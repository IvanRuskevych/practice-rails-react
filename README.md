# README

## step 1
```rails
rails new rails_react_recipe -d postgresql -j esbuild -c bootstrap -T
```
## step 2 database.yml
```rails
default: &default
  #adapter: sqlite3
  adapter: postgresql
  encoding: unicode
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: postgres1
  password: fsd8080
  host: localhost
  #timeout: 5000
```
## step 3 
```rails
rails db:create
```

## step 4
```rails
bin/dev
```

## step 5 — Installing Frontend Dependencies

```rails
yarn add react react-dom react-router-dom
```

## step 6 — Setting Up the Homepage

```rails
rails g controller Homepage index
```
* /config/routes.rb
```rails
Rails.application.routes.draw do
  root 'homepage#index'
  # For details on the DSL available within this file, see http://guides.rubyonrails.org/routing.html
end
```

* Remove the code inside the file, then save the file as empty. By doing this, you ensure that the contents of /app/views/homepage/index.html.erb do not interfere with the React rendering of your frontend.

## step 7 — Configuring React as Your Rails Frontend

* /app/javascript/application.js
```rails
// Entry point for the build script in your package.json
import "@hotwired/turbo-rails"
import "./controllers"
import * as bootstrap from "bootstrap"
import "./components"
```
* /app/javascript/routes/index.jsx
```rails
import React from "react";
import { BrowserRouter as Router, Routes, Route } from "react-router-dom";
import Home from "../components/Home";

export default (
  <Router>
    <Routes>
      <Route path="/" element={<Home />} />
    </Routes>
  </Router>
);
```

* /app/javascript/components/App.jsx
```rails
import React from "react";
import Routes from "../routes";

export default props => <>{Routes}</>; 
```

* /app/javascript/components/index.jsx
```rails
import React from "react";
import { createRoot } from "react-dom/client";
import App from "./App";

document.addEventListener("turbo:load", () => {
  const root = createRoot(
    document.body.appendChild(document.createElement("div"))
  );
  root.render(<App />);
});
```
* /app/javascript/components/index.jsx
* /app/assets/stylesheets/application.bootstrap.scss


This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...
