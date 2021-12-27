# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Changed
- Replaced all `/access` sub-paths with wildcard `/access/*`
- Renamed response `AuthorizedAccessToSingleRoute` to `AuthorizedAccessToResource`

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
