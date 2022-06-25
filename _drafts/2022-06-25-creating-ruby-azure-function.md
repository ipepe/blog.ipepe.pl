---
title: "Creating a Ruby Azure Function"
categories: ["ruby","ruby-on-rails","azure"]
---


To create azure function You need to have `func` cli tool installed.


## Running

1. `npm install`
2. `npm start`
3. `func start`

## Setup

1. `func init . --typescript`
2. `func new --name HttpExample --template "HTTP trigger" --authlevel "anonymous"`
3. `func azure functionapp publish <APP_NAME>`