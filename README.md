# Trébol eCommerce API
<!-- ALL-CONTRIBUTORS-BADGE:START - Do not remove or modify this section -->
[![All Contributors](https://img.shields.io/badge/all_contributors-2-orange.svg?style=flat-square)](#contributors-)
<!-- ALL-CONTRIBUTORS-BADGE:END -->

[![GitHub Super-Linter](https://github.com/trebol-ecommerce/api/workflows/Lint%20Code%20Base/badge.svg)](https://github.com/marketplace/actions/super-linter)

The contract that Trébol as a whole must comply with.

## Documentation

- [Most recent release](https://studio-ws.apicur.io/sharing/b0bc9a13-4e93-4be2-8636-108986e75ce4)
- [Unreleased changes](https://studio-ws.apicur.io/sharing/817cd752-6043-4a6e-a230-ac0d70d07a43) (quality may be inconsistent)

## Specification

Below is a short summary of all available paths and their purposes.

### `/access` - Permissions for the API consumer

- `/` [Bearer] - Lists all paths in `/data` that the API consumer has any level of access to
- `/{resource}` [Bearer] - Lists allowed CRUD operations on a given resource. Can contain any combination of these four: `create`, `read`, `update` and `delete`

### `/account` - Resources for the API consumer and their user account

- `/profile` [Bearer] - Fetch or update existing personal and contact information

### `/data` - CRUD operations

- `/billing_types` [Public] - Options for generating bill receipts
- `/customers` [Bearer] - Correlation of stored personal information towards clients that have actually requested to purchase through the store
- `/images` [Bearer] - Metadata of photos and pictures uploaded and served through any internal and/or external web service, assumed to be accesible from the internet
- `/people` [Bearer] - Stored contact and/or personal information about real-life individuals
- `/products` [Public] - The items that the store displays to the public and makes available for purchase. Includes products not available for purchase
- `/product_categories` [Public] - Tree-like schema of organization for products
- `/product_lists` [Public] - Named groups used to organize and link specific products together
- `/product_list_contents` [Public] - Pagination of products contained on given lists
- `/sales` [Bearer] - The purchases acknowledged through the store; they follow a certain transaction flow; updating their state to `requested`, `paid`, `cancelled`, `failed`, `delivered`, among others
  - `/confirmation` - [Bearer] - To indicate that a sell is ready for delivery/shipping
  - `/rejection` - [Bearer] - To indicate that a sell was acknowledged but cannot be completed. The customer should be refunded.
  - `/completion` - [Bearer] - To indicate that a sell has been delivered and it can be considered a success
- `/salespeople` [Bearer] - Correlation of stored personal information towards employees that earn sales through the store
- `/shippers` [Public] - Metadata of internal and/or external logistics services for shipping and delivery of physical items
- `/user_roles` [Bearer] - Metadata of available privilege groupings for users
- `/users` [Bearer] - Metadata of available accounts to access API resources

### `/public` - API resources that may not require auth

- `/about` [Public] - Metadata about the store and their respective owners
- `/checkout` [Bearer] - Transaction request; where consumers submit a cart with products and receive details to be redirected to the payment page.
  - `/validate` [Public] - Endpoint of return from payment page. Must redirect to a result page served through the corresponding frontend of the store.
- `/guest` [Public] - Request a short-lived token that can be used for calls to `/checkout`
- `/login` [Public] - Request for authentication with an existing user account, and generation + fetching of new auth token
- `/receipt/{code}` [Public] - Metadata for a specific `Sell`. The `code` variable must identify only one transaction, but its exact meaning can vary
- `/register` [Public] - Request for creation of a new user account

## Contributors ✨

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="http://benjaminlamadrid.cl"><img src="https://avatars.githubusercontent.com/u/68207359?v=4?s=100" width="100px;" alt=""/><br /><sub><b>bglamadrid</b></sub></a><br /><a href="#design-bglamadrid" title="Design">🎨</a></td>
    <td align="center"><a href="http://www.apicur.io/"><img src="https://avatars.githubusercontent.com/u/28107283?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Apicurio</b></sub></a><br /><a href="#tool-Apicurio" title="Tools">🔧</a></td>
  </tr>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!
