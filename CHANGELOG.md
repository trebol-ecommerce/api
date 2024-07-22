# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Changed

- [BREAKING CHANGE] In newly-named `Order`, `Customer` and `Salesperson` now reference a `Person` element instead
- [BREAKING CHANGE] Rename all instances of `Sell` to `Order`
  - Tag `sales` -> `orders`
  - Endpoint `/data/sales` -> `/data/orders`
    - All methods GET, POST, PUT and PATCH
    - All subroutes
      - `/confirmation`
      - `/rejection`
      - `/completion`
  - Schemas
    - `Sell` -> `Order`
    - `SellProperties` -> `OrderProperties`
    - `SellDetail` -> `OrderDetail`
    - `SellDetailProperties` -> `OrderDetailProperties`
  - All uses of the noun in literal descriptions

### Removed

- [BREAKING CHANGE] Elements that constitute the concepts of `Customer` and `Salesperson`
  - Endpoints `/data/customers` and `/data/salespeople`
  - Schemas `Customer` and `Salesperson`
  - Tags `customers` and `salespeople`

## [v1.7.3] - 2024-03-11

### Changed

- The following schemas were merged into their original ones
  - `ProductRequiredProperties` -> `Product`
  - `SellRequiredProperties` -> `Sell`
  - `UserRequiredProperties` -> `User`
  - `UserRoleRequiredProperties` -> `UserRole`
  - `ImageRequiredProperties` -> `Image`
  - `PersonRequiredProperties` -> `Person`
  - `ProductCategoryRequiredProperties` -> `ProductCategory`
  - `ProductListRequiredProperties` -> `ProductList`
  - `ShipperRequiredProperties` -> `Shipper`

## [v1.7.2] - 2023-05-26

### Fixed

- Bad $ref

## [v1.7.1] - 2023-05-26

### Fixed

- Joined specification documents back into one

## [v1.7.0] - 2023-05-24

### Added

- `PATCH` methods, to partially update data
  - affected endpoints
    - `/data/products`
    - `/data/sales`
    - `/data/users`
    - `/data/images`
    - `/data/product_categories`
    - `/data/shippers`
    - `/data/product_lists`
  - all of these are tagged with `partial-update`

### Changed

- To support `PATCH` methods, each and every CRUD-related schema was split into three
  - One schema only has the `properties` array from the original one, and is added the suffix `-Properties`
  - Another, with the `required` array, and is added the suffix `-RequiredProperties`
  - The last one extends from both the others, plus includes the rest of the metaproperties `name`, `description`, `example`, and retains the original name
  - All of this is true for these following schemas, resulting in the following new ones:
    - `Product` -> `ProductProperties` & `ProductRequiredProperties`
    - `Sell` -> `SellProperties` & `SellRequiredProperties`
    - `User` -> `UserProperties` & `UserRequiredProperties`
    - `Image` -> `ImageProperties` & `ImageRequiredProperties`
    - `ProductCategory` -> `ProductCategoryProperties` & `ProductCategoryRequiredProperties`
    - `Shipper` -> `ShipperProperties` & `ShipperRequiredProperties`
    - `ProductList` -> `ProductListProperties` & `ProductListRequiredProperties`
  - This way, each `PATCH` method only needs a `-Properties` schema, and each `PUT`/`POST` still makes use of the original schema.

### Fixed

- SuperLinter badge url

## [v1.6.1] - 2023-04-10

### Added

- SuperLinter GitHub Action

## [v1.6.0] - 2023-04-10

### Changed

- Created a second API document `common.trebol-api.json` for common components
  - Moved schemas to this document
    - `DataPage`
    - `LoginCredentials`
    - `UserRegistration`
    - `AuthorizedAccess`
    - `Person`
  - Moved responses to this document
    - `PaginatedCollection`
    - `Forbidden`
    - `AuthorizedAccessToResource`
    - `AuthorizedAccessToRoutes`
    - `NotFound`
    - `Empty`
    - `AllowMethodPOST`
    - `AllowMethodGET`
    - `AllowAllMethods`
    - `AllowMethodGET-PUT`
    - `BadRequestBody`
  - Rewritten References (`$ref`) to load all these components from the second document file if it exists in the same directory

## [v1.5.4] - 2023-03-27

### Changed

- Clean up unused resources
- Refactor (inline) schemas only used once

### Fixed

- Incorrect types for `/data/product_lists` (was using `ProductCategory`)

## [v1.5.1] - 2023-02-17

### Added

- Declare global tags

### Fixed

- Incongruent CRUD operations tags
  - `delete` and `remove` are now merged as `delete`
  - `fetch-one` and `fetch-many` are now called `read-one` and `read-many`

## [v1.5.0] - 2022-04-29

### Added

- Query parameters specification for `GET /data/product_lists`
  - `ProductList` specific query params are `code`, `name`, `codeLike` and `nameLike`
- Three resources to interact with processing of sales
  - `POST /data/sales/confirmation` - Should confirm a given sell that is in a `Paid` or similar state
  - `POST /data/sales/rejection` - Should reject a given sell that is in a `Paid` or similar state
  - `POST /data/sales/completion` - Should mark a sell as `Completed` or `Delivered`, given that it is in a `Confirmed` or similar state
- New query parameters for `GET /data/sales` - `afterDate`, `beforeDate` and `statusCode`

### Changed

- Removed some empty security schema specs

### Fixed

- Added missing data type ref to path parameter in `/access/{resource}` path
- Moved `date` query parameter for `/data/sales` to be used only in its `GET` method

### Removed

- Deprecated resource paths
  - `/public/categories` - Since v1.1.0
  - `/public/products` - Since v1.2.1
  - `/public/products/{barcode}` - Since v1.2.0

## [v1.2.2] - 2022-01-07

### Changed

- Means to use `/data/product_list_contents`
  - `POST` accepts a single `Product` entity at a time
  - Remove most query parameters from `PUT` and `POST`
    - Only keep `listCode` as globally supported
    - `GET` and `DELETE` do support them all
  - Update descriptions

## [v1.2.1] - 2021-12-29

### Fixed

- Incorrect request body specifications for `/data/product_list_contents`
- Added a security schema to all methods

### Changed

- Entity `ProductList`
  - made property `name` optional
- Methods in `/data` are now publicly available
  - `GET /data/billing_types`
  - `GET /data/products`
  - `GET /data/product_lists`
  - `GET /data/product_list_contents`
  - `GET /data/product_categories`
  - `GET /data/shippers`

### Deprecated

- Path `/public/products` will be superseded by `/data/products`

## [v1.2.0] - 2021-12-27

### Added

- New entity `ProductList`
  - with properties `code`, `name` and `totalCount`
- New path `/data/product_lists`
  - supports methods `GET`, `POST`, `PUT` and `DELETE`
- New path `/data/product_list_contents`
  - supports methods `GET`, `POST`, `PUT` and `DELETE`
  - requires `listCode` in query parameters

### Fixed

- Outdated response refs in some `OPTIONS` resources

### Changed

- Replaced all `/access` sub-paths with wildcard `/access/*`
- Renamed response `AuthorizedAccessToSingleRoute` to `AuthorizedAccessToResource`
- Renamed category-related query parameters in `/data/products`
  - `productCategory` to `categoryCode`
  - `productCategoryLike` to `categoryCodeLike`

### Deleted

- Paths marked for deprecation:
  - `/data/customers/{idNumber}`
  - `/data/images/{code}`
  - `/data/product_categories/{parentCode}`
  - `/data/products/{barcode}`
  - `/data/sales/{buyOrder}`
  - `/data/salespeople/{idNumber}`
  - `/data/users/{name}`
  - `/public/categories/{parentId}`

### Deprecated

- Path `/public/products/{barcode}` should be superseded with query parameters

## [v1.1.3] - 2021-12-27

### Fixed

- Use ref to predefined response for `/public/register [200 OK]`
- Missing examples for some specifications of `sort` as a query parameter

### Changed

- Several parameter descriptions

## [v1.1.2] - 2021-12-07

### Changed

- Entity `ProductCategory` and Path `/data/product_categories`
  - property & query parameter `code` changed from type `integer` to `string`
  - query parameter `parentCode` changed from type `integer` to `string`
- All GET resources within `/data` include pagination parameters `pageIndex`, `pageSize`, `sortBy`, `sortOrder`

## [v1.1.1] - 2021-10-24

### Added

- Entity `Receipt`
  - introduce properties `token`, `taxValue`, `transportValue` and `totalItems`

### Changed

- Entity `Receipt`
  - rename `amount` property to `totalValue`
  - require properties `token` and `totalItems` in addition to base schema properties

### Fixed

- Entity `Sell`
  - include missing property `transportValue` - _this was wrongly documented as an addition in v1.1.0; changelog was updated_

## [v1.1.0] - 2021-10-20

### Added

- Path `/data/product_categories`
  - include methods `GET`, `POST`, `PUT` and `DELETE` to manage product categories
- Path `/data/shippers`
  - include method  `GET`, `POST`, `PUT` and `DELETE` to manage shippers
- Entity `Sell`
  - introduce properties `token`, `taxValue`, `totalValue` and `totalItems`
- Entity `SellDetail`
  - introduce property `unitValue`

### Changed

- Entity `Person`
  - [__Breaking change__] Property `name` split into two, `firstName` and `lastName`
- Paths in `/data` without path parameters
  - updated summary and description
  - paging query parameters are now (aptly) named `pageSize` and `pageIndex`

### Deprecated

__The following will be removed in the minor version that follows this one.__
Please follow given advices and use corresponding replacements before that.

- Reduce redundant API resources
  - `/public/categories` - use `/data/product_categories` instead
  - `/public/categories/{parentId}` - use `/data/product_categories?parentCode={}` instead
- Replace parameterized paths with simpler paths and use of query parameters (for all available methods)
  - `/data/customers/{idNumber}` - use `/data/customers?idNumber={}` instead
  - `/data/images/{code}` - use `/data/images?code={}` instead
  - `/data/products/{code}` - use `/data/products?barcode={}` instead
  - `/data/sales/{buyOrder}` - use `/data/sales?buyOrder={}` instead
  - `/data/salespeople/{idNumber}` - use `/data/salespeople?idNumber={}` instead
  - `/data/users/{name}` - use `/data/users?name={}` instead

### Removed

- All `500 Internal Server Error` responses, and the `UnknownError` predefined response

## [v1.0.5] - 2021-10-19

### Added

- Tags
  - add entity tags to entity-related resources, such as `products`, `customers` and `sales`

### Changed

- Path `/data/people`
  - change `operationId`
- Tags
  - instead of `fetch`, `one`, `many` and `existing`, only use `fetch-one` and `fetch-many`

## [v1.0.4] - 2021-10-19

### Added

- Entity `Product`: include property `description` as `string`

### Changed

- Entity `Address`
  - require properties `firstLine`, `municipality` and `city` as base schema information
- Entity `BillingCompany`
  - require property `idNumber` as base schema information
- Entity `Image`
  - require properties `filename`, `url` and `code` as base schema information
  - set `code` data type to `string`
- Entity `Product`
  - require properties `barcode` as base schema information
- Entity `ProductCategory`
  - require property `name` as base schema information
  - fix example
- Entity `Receipt`
  - require properties `amount`, `buyOrder`, `date`, and `status` as base schema information
  - remove `format` metadata from `buyOrder` and `amount`
- Entity `Sell`
  - add description
  - require property `details` in addition to others as base schema information
  - update description of `billingCompany` property
- Entity `SellDetail`
  - require properties `product` and `units` as base schema information
  - add description to both properties
  - remove `format` metadata from `units` property
- Entity `SellStatus`
  - add description
  - require properties `code` and `name`
  - add description to both properties
  - update data type of `code` to `integer`
- Entity `Shipper`
  - add description
  - add description to `name` property
- Entities `ShopOwnerDetails`, `User` and `UserRole`
  - update description
- Entities `Customer` and `Salesperson`
  - require property `person` as base schema information
  - add a description to `person` property
- Entities `PaymentType` and `BillingType`
  - require property `name` as base schema information

## [v1.0.3] - 2021-09-21

### Added

- Entity `Sell`
  - include required property `customer` as `Person`

## [v1.0.2] - 2021-09-20

### Changed

- Path `/data/product_categories/{parentId}`
  - parameter `parentId` renamed to `parentCode`
- Entity `ProductCategory`
  - property `id` renamed to `code`

## [v1.0.1] - 2021-09-20

### Added

- Entity `User`
  - require property `name` as base schema information
  - include property `role` as `string`


## [v1.0.0] - 2021-09-20

First public version.
