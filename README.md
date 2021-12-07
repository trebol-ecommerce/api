# The Trébol backend API
<!-- ALL-CONTRIBUTORS-BADGE:START - Do not remove or modify this section -->
[![All Contributors](https://img.shields.io/badge/all_contributors-2-orange.svg?style=flat-square)](#contributors-)
<!-- ALL-CONTRIBUTORS-BADGE:END -->

Declares the resources that instances of the Trébol backend must expose. [Review the documentation here.](https://studio-ws.apicur.io/sharing/b0bc9a13-4e93-4be2-8636-108986e75ce4)

This API has been designed using [APICurio](https://www.apicur.io/), a beautiful web platform and free service made for the job.

## Specification

Below is a short summary of available paths and their purposes. Unless stated otherwise, they all impose the need of a Bearer token auth.

### `/access` - Allowed privileges for the API consumer

- `/` - Lists all paths in `/data` that the API consumer has any level of access to
- `/{context}` - Lists allowed CRUD operations on a given context. Can contain any combination of these four: `create`, `read`, `update` and `delete`

### `/account` - Resources for the API consumer and their user account

- `/profile` - Fetch or update existing personal and contact information

### `/data` - Execution of CRUD operations for all supported contexts

- `/billing_types` - Options for generating bill receipts
- `/customers` - Correlation of stored personal information towards clients that have actually requested to purchase through the store
- `/images` - Metadata of photos and pictures uploaded and served through any internal and/or external web service, assumed to be accesible from the internet
- `/people` - Stored contact and/or personal information about real-life individuals
- `/product_categories` - Tree-like schema of organization for products
- `/products` - The items that the store displays to the public and makes available for purchase. Includes products not available for purchase
- `/sales` - The purchases acknowledged through the store; they follow a certain transaction flow; updating their state to `requested`, `paid`, `cancelled`, `failed`, `delivered`, among others
- `/salespeople` - Correlation of stored personal information towards employees that earn sales through the store
- `/shippers` - Metadata of internal and/or external logistics services for shipping and delivery of physical items
- `/user_roles` - Metadata of available privilege groupings for users
- `/users` - Metadata of available accounts to access API resources

### `/public` - API resources that may not require auth

- `/about` - Metadata about the store and their respective owners
- `/checkout` - (Needs auth) Transaction request; where consumers submit a cart with products and receive details to be redirected to the payment page.
  - `/validate` - Endpoint of return from payment page. Must redirect to a result page served through the corresponding frontend of the store.
- `/guest` - Request a short-lived auth token that can be used for calls to `/checkout`
- `/login` - Request for authentication with an existing user account, and generation + fetching of new auth token
- `/products` - Similar to `/data/products`, but will only fetch products available to the public
- `/receipt/{code}` - Metadata for a specific `Sell`. The `code` variable must identify only one transaction, but its exact meaning can vary
- `/register` - Request for creation of a new user account

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
