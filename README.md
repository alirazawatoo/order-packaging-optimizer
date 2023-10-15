# Order Packaging Optimizer

A Rails application for managing products, package definitions, and orders, then selecting packages for an order through a dedicated service object.

## Workflow

```text
products + package capacities -> order line items -> PackageSelector -> suggested packages
```

The application provides browser CRUD for products, packages, and orders. `app/services/package_selector.rb` contains the selection policy, keeping packaging decisions outside controllers and models.

## Local setup

```bash
bundle install
npm install
rails db:create db:migrate db:seed
rails server
```

Configure PostgreSQL credentials through the environment expected by `config/database.yml`.

## Decision boundary

The selector implements the repository's current packing rules; it is not presented as a mathematically optimal bin-packing solver. A useful evaluation should state package dimensions/capacities, product quantities, ordering rules, and tie-breaking explicitly.

RSpec coverage is present for models, requests, and services. Concurrency, inventory constraints, shipping cost, and large-order performance remain outside the demonstrated scope.
