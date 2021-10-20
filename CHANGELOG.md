# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Path `/data/product_categories`: include method `POST` for creating new categories
- Path `/data/product_categories/{parentCode}` with methods `GET`, `PUT` and `DELETE`, to manage product categories

### Changed
- __Breaking change__: Entity `Person`: property `name` split into two, `firstName` and `lastName`
- Paths in `/data` without path parameters: Updated summary and description; paging query parameters are now aptly named `pageSize` and `pageIndex`

### Deprecated
These will be unsupported in the minor version that follows this one.
Follow given advices and use corresponding replacements for all use cases involved.

- Reducing redundant API resources
  - `/public/categories`: use `/data/product_categories` instead
  - `/public/categories/{parentId}`: use `/data/product_categories/{parentCode}` instead
- Replacing parameterized paths with simpler paths and use of query parameters (all available methods apply)
  - `/data/customers/{idNumber}`: use `/data/customers?idNumber={}` instead
  - `/data/images/{code}`: use `/data/images?code={}` instead
  - `/data/product_categories/{parentCode}`: use `/data/product_categories?parentCode={}` and `/data/product_categories?code={}` instead
  - `/data/products/{code}`: use `/data/products?barcode={}` instead
  - `/data/sales/{buyOrder}`: use `/data/sales?buyOrder={}` instead
  - `/data/salespeople/{idNumber}`: use `/data/salespeople?idNumber={}` instead
  - `/data/users/{name}`: use `/data/users?name={}` instead

## [1.0.5] - 2021-10-19

### Added
- Add entity tags to entity-related resources, such as `products`, `customers` and `sales`

### Changed
- Path `/data/people`: change `operationId`
- Update tags:
  - remove `fetch`, `one`, `many` and `existing`
  - add `fetch-one` and `fetch-many`


## [1.0.4] - 2021-10-19

### Added
- Entity `Product`: include property `description` as `string`

### Changed
- Entity `Address`: require properties `firstLine`, `municipality` and `city` as base schema information
- Entity `BillingCompany`: require property `idNumber` as base schema information
- Entity `Image`: require properties `filename`, `url` and `code` as base schema information; set `code` data type to `string`
- Entity `Product`: require properties `barcode` as base schema information
- Entity `ProductCategory`: require property `name` as base schema information; fix example
- Entity `Receipt`: require properties `amount`, `buyOrder`, `date`, and `status` as base schema information; remove `format` metadata from `buyOrder` and `amount`
- Entity `Sell`: include description; require property `details` in addition to others as base schema information; update description of `billingCompany` property
- Entity `SellDetail`: require properties `product` and `units` as base schema information; add description to both; remove `format` metadata from `units`
- Entity `SellStatus`: add description, require properties `code` and `name`, include descriptions of both, update data type of `code` to `integer`
- Entity `Shipper`: add description, include description of property `name`
- Entities `ShopOwnerDetails`, `User` and `UserRole`: update description
- Entities `Customer` and `Salesperson`: require property `person` as base schema information; add a description to it
- Entities `PaymentType` and `BillingType`: require property `name` as base schema information


## [1.0.3] - 2021-09-21

### Added
- Entity `Sell`: include required property `customer` as `Person`


## [1.0.2] - 2021-09-20

### Changed
- Path `/data/product_categories/{parentId}`: parameter `parentId` renamed to `parentCode`
- Entity `ProductCategory`: property `id` renamed to `code`


## [1.0.1] - 2021-09-20

### Added
- Entity `User`: require property `name` as base schema information; include property `role` as `string`


## [1.0.0] - 2021-09-20

First public version.
