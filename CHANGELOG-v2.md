# Release Notes for Craft Commerce 2.x

## Unreleased

### Added
- Added the ability to place a note on a refund transaction.
- Added the `craft\commerce\services\TaxCategories::getAllTaxCategoriesAsList()` method.

### Fixed
- Fixed a javascript error on the Edit Product Type screen.
- Fixed a bug where states were not saving on the Store Location page.

## 2.0.0-beta.3 - 2018-04-17

### Added
- Added the `craft\commerce\elements\Order::EVENT_AFTER_ADD_LINE_ITEM` event.

### Fixed
- Fixed a bug where variant fields did not appear on the Edit Product page if no product fields existed. ([#317](https://github.com/craftcms/commerce/issues/317))
- Fixed a bug where subscription payment details were not being syntax-highlighted.
- Fixed a PHP error that occurred when saving the primary payment currency while using PostgreSQL.
- Fixed a bug where trial status was being incorrectly reported by subscriptions.
- Fixed a bug where it was impossible to pay with a stored payment source.

## 2.0.0-beta.2 - 2018-04-10

### Added
- Added `craft\commerce\elements\db\VariantQuery::hasSales()`.

### Fixed
- Fixed a bug on the Edit Order page where the info buttons on line items were unresponsive. ([#297](https://github.com/craftcms/commerce/issues/297))
- Fixed a bug where customer addresses were not editable from the Edit User page. ([#315](https://github.com/craftcms/commerce/issues/315))
- Fixed a PHP error that occurred when submitting a payment source at checkout. ([#313](https://github.com/craftcms/commerce/issues/313))
- Fixed a PHP error that occurred when submitting a gateway choice at checkout. ([#312](https://github.com/craftcms/commerce/issues/312))
- Fixed a PHP error that occurred when calling `count()` on a variant query. 
- Fixed a PHP 7.0 compatibility issue. ([#305](https://github.com/craftcms/commerce/issues/305))
- Fixed a PHP 7.2 compatibility issue. ([#308](https://github.com/craftcms/commerce/issues/308))

## 2.0.0-beta.1.3 - 2018-04-05

### Fixed
- Fixed a PHP error that occurred when purging abandoned carts without an email.

## 2.0.0-beta.1.2 - 2018-04-05

### Changed
- Updating from Commerce 1.x now requires that Commerce 1.2.1360 or greater is installed.

### Fixed
- Fixed an SQL error that occurred when updating from Commerce 1.x that had existing discounts. ([#299](https://github.com/craftcms/commerce/issues/299))
- Fixed currency editing template where it was calling deprecated methods ([#303](https://github.com/craftcms/commerce/issues/303))

## 2.0.0-beta.1.1 - 2018-04-04

### Fixed
- Fixed a bug where visiting the payment currencies settings page could result in fatal error on new installs.
- Fixed a SQL error that occurred when installing Commerce.
- Fixed a SQL error that occurred when updating from Commerce 1.x.

## 2.0.0-beta.1 - 2018-04-04

### Added
- Added 'Copy' Reference tag to Product actions.
- Added the possibility for users to save payment sources.
- Added subscriptions features for gateways that support them.
- Added `craft\commerce\services\PaymentSources` service.
- Added `craft\commerce\services\Plans` service.
- Added `craft\commerce\services\Subscriptions` service.
- Added additional ways for sales to affect the price of matching products.
- Added `paidStatus` attribute to the Order element.
- Added `craft.variants` twig variable which returns the new VariantQuery class.
- Added `craft.subscriptions` twig variable which returns the new SubscriptionQuery class.
- Added the ability for any purchasable to have sales.
- Added ability to have sales applied based on a Craft category related to a purchasable.
- Added `craft\commerce\models\Customer::getPrimaryBillingAddress()`
- Added `craft\commerce\models\Customer::getPrimaryShippingAddress()`
- Added `craft\commerce\services\Address::getAddressByIdAndCustomerId()`
- Added `craft\commerce\services\Customers::setLastUsedAddresses()`

### Changed
- Removed the `cartCookieDuration` config item. All carts are now related to php session. 
- Replaced`customer.lastUsedShippingAddress` and `customer.lastUsedBillingAddress` with `customer.primaryBillingAddress` and `customer.primaryShippingAddress`
- Removed `baseShipping`, `baseDiscount`, `baseTax`, `baseTaxIncluded` attributes from the order model. Order's now have order level adjustments.
- Removed `shipping`, `discount`, `tax`, `taxIncluded` attributes from the line item model. Line item's now have line item level adjustments.
- The Shipping Rule interface now expects a shipping category ID passed to each rate method.
- `paymentMethodSettings` setting is now called `gatewaySettings` and it now uses handles to reference gateways instead of IDs.
- `Payment Methods` are now called `Gateways` and this is reflected across the entire plugin and it's API.
- `sendCartInfoToGateways` is now called `sendCartInfo` and is a per-gateway setting.
- `requireEmailForAnonymousPayments` config setting removed as completed order now always require the correct email address to make anonymous payments on orders.
- `Variant::setSalesApplied()` and `Variant::getSalesApplied()` is now called `Variant::setSales()` and `Variant::getSales()` respectively.
- `OrderAdjustment::optionsJson` is now called `OrderAdjustment::sourceSnapshot`.
- Removed the purchasable interface `PurchasableInterface::validateLineItem()`. Your purchasables should now use `PurchasableInterface::getLineItemRules()` to add validation rules to line items. 
- The payment method overrides in commerce.php config file have been moved to a commerce-gateway.php config file.
- Vat ID validation is now using the MIT licenced dannyvankooten/vat.php
- The `Variants::EVENT_PURCHASE_VARIANT` event has been replaced by `ElementInterface::afterOrderComplete($lineItem)`
- `craft\commerce\services\Cart` is now `craft\commerce\services\Carts`
- `craft\commerce\services\Carts::addToCart()` now requires a `craft\commerce\models\LineItem` object as the second parameter.
- `craft\commerce\services\LineItems::getLineItemByOrderPurchasableOptions()` is now `craft\commerce\services\LineItems::resolveLineItem()`
- `craft\commerce\services\Pdf::pdfForOrder()` is now `craft\commerce\services\Pdf::renderPdfForOrder()`
- Last addresses used by customers are no longer stored. Instead, customers have primary shipping and billing addresses.
- `craft\commerce\elements\Orders` now fires the following events: `beforeCompleteOrder`, and `afterCompleteOrder`.
- `craft\commerce\services\Addresses` now fires the following events: `beforeSaveAddress`, and `afterSaveAddress`.
- `craft\commerce\services\Carts` now fires the following events: `beforeAddToCart`, `afterAddToCart`, `afterRemoveFromCart` and a cancelable `beforeRemoveFromCart` event.
- `craft\commerce\services\Discounts` now fires the cancelable `beforeMatchLineItem` event.
- `craft\commerce\services\Emails` now fires the following events: `afterSendEmail`, and a cancelable `beforeSendEmail`.
- `craft\commerce\services\LineLitems` now fires the following events: `beforeSaveLineItem`, `afterSaveLineItem`, `createLineItem`, and `populateLineItem`.
- `craft\commerce\services\OrderHistories` now fires the `orderStatusChange` event.
- `craft\commerce\services\Payments` now fires the following events: `beforeCaptureTransaction`, `afterCaptureTransaction`, `beforeRefundTransaction`, `afterRefundTransaction`, `afterProcessPaymentEvent` and a cancelable `beforeProcessPaymentEvent` event.
- `craft\commerce\services\PaymentSources` now fires the following events: `deletePaymentSource`, `beforeSavePaymentSource` and `afterSavePaymentSource`events.
- `craft\commerce\services\Plans` fires the following events: `archivePlan`, `beforeSavePlan` and `afterSavePlan`events.
- `craft\commerce\services\Purchasables` fires the `registerPurchasableElementTypes` event.
- `craft\commerce\services\Sales` now fires the cancelable `beforeMatchPurchasableSale` event.
- `craft\commerce\services\Subscriptions` fires the `expireSubscription`, `afterCreateSubscription`, `afterReactivateSubscription`, `afterSwitchSubscriptionPlan`, `afterCancelSubscription`, `beforeUpdateSubscription`, `receiveSubscriptionPayment` and cancelable `beforeCreateSubscription`, `beforeReactivateSubscription`, `beforeSwitchSubscriptionPlan` and `beforeCancelSubscription` events.
- `craft\commerce\services\Transactions` now fires the `afterSaveTransaction` event.
- `craft\commerce\services\Variants` now fires the `purchaseVariant` event.
- Instead of the `commerce_modifyEmail` hook you should use the cancelable `beforeSendEmail` event fired by `craft\commerce\services\Emails`.
- Instead of the `commerce_registerOrderAdjusters` hook you should use the `registerOrderAdjusters` event fired by `craft\commerce\services\OrderAdjustments`.
- To register new gateway types, use the `registerGatewayTypes` event fired by `craft\commerce\services\Gateways`.
- The `commerce_modifyOrderSources`, `commerce_getOrderTableAttributeHtml`, `commerce_getProductTableAttributeHtml`, `commerce_defineAdditionalOrderTableAttributes`, `commerce_defineAdditionalProductTableAttributes` hooks have been replaced by more generic Craft 3 hooks.

### Removed
- Removed `craft\commerce\services\Countries::getCountryByAttributes()`
- Removed `craft\commerce\services\States::getStatesByAttributes()`
- Removed `craft\commerce\models\Customer::getLastUsedBillingAddress()`
- Removed `craft\commerce\models\Customer::getLatUsedShippingAddress()`
- Removed the `commerce_modifyGatewayRequestData`, `commerce_modifyGatewayRequestData` and `commerce_modifyItemBag` hooks.
