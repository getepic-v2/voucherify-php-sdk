<p align="center" >
  <img src="./docs/images/voucherify-php-sdk.png" />
</p>

<h3 align="center">Official <a href="http://voucherify.io?utm_source=github&utm_medium=sdk&utm_campaign=acq">Voucherify</a> SDK for PHP</h3>

<hr />

<p align="center">
<b><a href="#migration-from-0x">Migration from 0.x</a></b>
|
<b><a href="#setup">Setup</a></b>
|
<b><a href="#error-handling">Error handling</a></b>
|
<b><a href="#contributing">Contributing</a></b>
|
<b><a href="#changelog">Changelog</a></b>
</p>

<p align="center">
API:
<a href="#vouchers-api">Vouchers</a>
|
<a href="#campaigns-api">Campaigns</a>
|
<a href="#distributions-api">Distributions</a>
|
<a href="#validations-api">Validations</a>
|
<a href="#redemptions-api">Redemptions</a>
|
<a href="#customers-api">Customers</a>
|
<a href="#orders-api">Orders</a>
|
<a href="#products-api">Products</a>
|
<a href="#validation-rules-api">Validation Rules</a>
|
<a href="#segments-api">Segments</a>
|
<a href="#events-api">Events</a>
|
<a href="#promotions-api">Promotions</a>
|
<a href="#async-actions-api">Async Actions</a>
|
<a href="#utils">Utils</a>
</p>

## Setup

Add Voucherify dependency into your `composer.json`:
```
"rspective/voucherify": "v2.0.*"
```
Update project dependencies:

```
$ composer install
```
[Log-in](http://app.voucherify.io/#/login) to Voucherify web interace and obtain your Application Keys from [Configuration](https://app.voucherify.io/#/app/configuration):

```php
require_once('vendor/autoload.php');

use Voucherify\VoucherifyClient;
use Voucherify\ClientException;

$apiID  = "YOUR-APPLICATION-ID";
$apiKey = "YOUR-CLIENT-SECRET-KEY";

$client = new VoucherifyClient($apiID, $apiKey);
```

### Versioning
All requests will use your account API settings, unless you override the API version. The changelog lists every available version.

```php
$apiVersion = "v2018-08-01";

$client = new VoucherifyClient($apiID, $apiKey, $apiVersion);
```

Check [versioning](https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#versioning).

### Custom API URL
By default client is sending request to `https://api.voucherify.io`. You can override `$apiUrl` while creating client instance if you want to use Voucherify running in a specific region

```php
$apiVersion = null;
$apiUrl = "https://<region>.api.voucherify.io";

$client = new VoucherifyClient($apiID, $apiKey, $apiVersion, $apiUrl);
```

### Custom Headers
It is possible to send custom headers in Voucherify API request.
```php
$apiVersion = null;
$apiUrl = null;
$customHeaders = [
    "X-Custom-1" => "Value-1"
];

$client = new VoucherifyClient($apiID, $apiKey, $apiVersion, $apiUrl, $customHeaders);

# RESULT:
#   x-custom-1: Value-1
```

Special: Voucherify-Channel customization
```php
$apiVersion = null;
$apiUrl = null;
$customHeaders = [
    "V-Voucherify-Channel" => "Value-1"
];

$client = new VoucherifyClient($apiID, $apiKey, $apiVersion, $apiUrl, $customHeaders);

# RESULT:
#   x-voucherify-channel: PHP-SDK-Value-1
```

### PHP autoloading

When you aren't using composer you can load Voucherify module by including `autoload.php` file from `/src` directory.

```php
require_once('{voucherify_src_path}/autoload.php');

use Voucherify\VoucherifyClient;
use Voucherify\ClientException;

$client = new VoucherifyClient($apiID, $apiKey);
```

## API

This SDK is fully consistent with restufl API Voucherify provides.
Detalied description and example responses  you will find at [official docs](https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq).
Method headers point to more detalied params description you can use.

### Vouchers API
Methods are provided within `$client->vouchers->*` namespace.
- [Create Voucher](#create-voucher)
- [Get Voucher](#get-voucher)
- [Update Voucher](#update-voucher)
- [Delete Voucher](#delete-voucher)
- [List Vouchers](#list-vouchers)
- [Enable Voucher](#enable-voucher)
- [Disable Voucher](#disable-voucher)
- [Add balance to Gift-Card Voucher](#add-balance-to-gift-card-voucher)
- [Import Vouchers](#import-vouchers)

Check [voucher object](https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#the-voucher-object).

#### [Create Voucher]
```php
$client->vouchers->create($voucher);
```
#### [Get Voucher]
```php
$client->vouchers->get($code);
```
#### [Update Voucher]
```php
$client->vouchers->update($voucher_update);
```
#### [Delete Voucher]
```php
$client->vouchers->delete($code);
$client->vouchers->delete($code, $force);
```
#### [List Vouchers]
```php
$client->vouchers->getList();
$client->vouchers->getList($params);
```
#### [Enable Voucher]
```php
$client->vouchers->enable($code);
```
#### [Disable Voucher]
```php
$client->vouchers->disable($code);
```
#### [Add balance to Gift-Card Voucher]
```php
$client->vouchers->addBalance($code, $balance);
```
#### [Import Vouchers]
```php
$client->vouchers->import($vouchers);
```

---

### Campaigns API

Methods are provided within `$client->campaigns->*` namespace.

- [Create Campaign](#create-campaign)
- [Get Campaign](#get-campaign)
- [Add Voucher to Campaign](#add-voucher-to-campaign)
- [Add Voucher with certain code to Campaign](#add-voucher-with-certain-code-to-campaign)
- [Import Vouchers to Campaign](#import-vouchers-to-campaign)
- [Delete Campaign](#delete-campaign)

#### [Create Campaign]
```php
$client->campaigns->create($campaign);
```
#### [Get Campaign]
```php
$client->campaigns->get($name);
```
#### [Add Voucher to Campaign]
```php
$client->campaigns->addVoucher($campaignName);
$client->campaigns->addVoucher($campaignName, $params);
```
#### [Add Voucher with certain code to Campaign]
```php
$client->campaigns->addVoucherWithCode($campaignName, $code);
$client->campaigns->addVoucherWithCode($campaignName, $code, $params);
```
#### [Import Vouchers to Campaign]
```php
$client->campaigns->importVouchers($campaignName, $vouchers);
```
#### [Delete Campaign]
```php
$client->campaigns->delete($campaignName);
```

---

### Distributions API
Methods are provided within `$client->distributions->*` namespace.

- [Publish Voucher](#publish-voucher)
- [Create Export](#create-export)
- [Get Export](#get-export)
- [Delete Export](#delete-export)
- [List Publications](#list-publications)

#### [Publish Voucher]
```php
$client->distributions->publish($campaign_name);
$client->distributions->publish($params);
```
#### [Create Export]
```php
$client->distributions->createExport($params);
```
#### [Get Export]
```php
$client->distributions->getExport($exportId);
```
#### [Delete Export]
```php
$client->distributions->deleteExport($exportId);
```
#### [List Publications]
```php
$client->distributions->getPublications();
$client->distributions->getPublications($params);
```

---

### Validations API
Methods are provided within `$client->validations->*` namespace.

- [Validate Voucher](#validate-voucher)
- [Validate Promotion Campaign](#validate-promotions-1)

#### [Validate Voucher]
```php
$client->validations->validate($code);
$client->validations->validate($code, $params);

// OR

$client->validations->validateVoucher($code);
$client->validations->validateVoucher($code, $params);
```

#### [Validate Promotion Campaign]
```php
$client->validations->validate($params);
```

---

### Redemptions API
Methods are provided within `$client->redemptions->*` namespace.

- [Redeem Voucher](#redeem-voucher)
- [Redeem Promotion's Tier](#redeem-promotion-tier)
- [Get Redemption](#get-redemption)
- [List Redemptions](#list-redemptions)
- [Get Voucher's Redemptions](#get-vouchers-redemptions)
- [Rollback Redemption](#rollback-redemption)

Check [redemption rollback object](https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#the-redemption-rollback-object).

#### [Redeem Voucher]
```php
$client->redemptions->redeem($code);
$client->redemptions->redeem($code, $params);
```
#### [Redeem Promotion's Tier]
```php
$client->redemptions->redeem($promotionsTier, $params);
```
#### [Get Redemption]
```
$client->redemptions->get($redemptionId);
```
#### [List Redemptions]
```php
$client->redemptions->getList();
$client->redemptions->getList($params);
```
#### [Get Voucher's Redemptions]
```php
$client->redemptions->getForVoucher($code);
```
#### [Rollback Redemption]
```php
$client->redemptions->rollback($redemption_id);
$client->redemptions->rollback($redemption_id, $params);
$client->redemptions->rollback($redemption_id, $reason);
```

---

### Customers API
Methods are provided within `$client->customers->*` namespace.

- [Create Customer](#create-customer)
- [Get Customer](#get-customer)
- [Update Customer](#update-customer)
- [Delete Customer](#delete-customer)
- [List Customers](#list-customers)

Check [customer object](https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#the-customer-object).

#### [Create Customer]
```php
$client->customers->create($customer);
```
#### [Get Customer]
```php
$client->customers->get($customer_id);
```
#### [Update Customer]
```php
$client->customers->update($customer_update);
```
#### [Delete Customer]
```php
$client->customers->delete($customer_id);
```
#### [List Customers]
```php
$client->customers->getList();
$client->customers->getList($params);
```

---

### Orders API
Methods are provided within `$client->orders->*` namespace.

- [Create Order](#create-order)
- [Get Order](#get-order)
- [Update Order](#update-order)
- [List Orders](#list-orders)

Check [customer object](https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#the-order-object).

#### [Create Order]
```php
$client->orders->create($order);
```
#### [Get Order]
```php
$client->orders->get($order_id);
```
#### [Update Order]
```php
$client->orders->update($order_update);
```
#### [List Orders]
```php
$client->orders->getList();
```

---

### Products API
Methods are provided within `$client->products->*` namespace.

- [Create Product](#create-product)
- [Get Product](#get-product)
- [List Products](#list-products)
- [Update Product](#update-product)
- [Delete Product](#delete-product)
- [Create SKU](#create-sku)
- [Get SKU](#get-sku)
- [List SKUs](#list-skus)
- [Update SKU](#update-sku)
- [Delete SKU](#delete-sku)

Check [product object](https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#the-product-object).

Check [sku object](https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#the-sku-object).

#### [Create Product]
```php
$client->products->create($product);
```
#### [Get Product]
```php
$client->products->get($product_id);
```
#### [List Products]
```php
$client->products->getList();
```
#### [Update Product]
```php
$client->products->update($product_update);
```
#### [Delete Product]
```php
$client->products->delete($product_id);
$client->products->delete($product_id, $force);
```
#### [Create SKU]
```php
$client->products->createSku($product_id, $sku);
```
#### [Get SKU]
```php
$client->products->getSku($product_id, $sku_id);
```
#### [List SKUs]
```php
$client->products->getSkus($product_id);
```
#### [Update SKU]
```php
$client->products->updateSku($product_id, $sku_update);
```
#### [Delete SKU]
```php
$client->products->deleteSku($product_id, $sku_id);
$client->products->deleteSku($product_id, $sku_id, $force);
```

---

### Validation Rules API
Methods are provided within `$client->validationRules->*` namespace.

- [Create Validation Rule](#create-validation-rule)
- [Get Validation Rule](#get-validation-rule)
- [Update Validation Rule](#update-validation-rule)
- [Delete Validation Rule](#delete-validation-rule)

Check [validation rule object](https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#the-validation-rule-object).

#### [Create Validation Rule]
```php
$client->validationRules->create($rule);
```
#### [Get Validation Rule]
```php
$client->validationRules->get($rule_id);
```
#### [List Validation Rules]
```php
$client->validationRules->getList();
```
#### [Update Validation Rule]
```php
$client->validationRules->update($rule_update);
```
#### [Delete Validation Rule]
```php
$client->validationRules->delete($rule_id);
```
#### [Create Validation Rule Assignment]
```php
$client->validationRules->createAssignment($rule_id, $assignment);
```
#### [List Validation Rule Assignments]
```php
$client->validationRules->getAssignments($rule_id);
```
#### [Delete Validation Rule Assignment]
```php
$client->validationRules->deleteAssignment($rule_id, $assignment_id);
```

---

### Segments API
Methods are provided within `$client->segments->*` namespace.

- [Create Segment](#create-segment)
- [Get Segment](#get-segment)
- [Delete Segment](#delete-segment)

Check [segment object](https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#the-segment-object).

#### [Create Segment]
```php
$client->segments->create($params);
```
#### [Get Segment]
```php
$client->segments->get($segment_id);
```
#### [Delete Segment]
```php
$client->segments->delete($segment_id);
```

---
### Events API
Methods are provided within `$client->customEvents->*` namespace.
- [Track Custom Event](#track-custom-event)

Check [event object](https://docs.voucherify.io/reference/the-custom-event-object?utm_source=github&utm_medium=sdk&utm_campaign=acq).

#### [Track Custom Event]
```php
$client->customEvent->track($event, $customer);
```

---

### Promotions API
Methods are provided within `$client->promotions->*` namespace.

- [Create Promotion Campaign](#create-promotion-campaign)
- [Validate Promotion Campaign](#validate-promotion-campaign)
- [List Promotion's Tiers](#list-promotions-tiers)
- [Create Promotion's Tier](#create-promotions-tier)
- [Redeem Promotion's Tier](#redeem-promotions-tier)
- [Update Promotion's Tier](#update-promotions-tier)
- [Delete Promotion's Tier](#delete-promotions-tier)
- [List Available Promotion Tiers](#list-available-promotion-tiers)

Check [promotion campaign object](https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#create-promotion-campaign).

Check [promotion's tier object](https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#the-promotion-object).

#### [Create Promotion Campaign]
```php
$client->promotions->create($promotionCampaign);
```

#### [Validate Promotion Campaign]
```php
$client->promotions->validate($validationContext);
```

#### [List Promotion's Tiers]
```php
$client->promotions->tiers->getList($promotionCampaignId);
```

#### [Create Promotion's Tier]
```php
$client->promotions->tiers->create($promotionCampaignId, $promotionsTier);
```

#### [Redeem Promotion's Tier]
```php
$client->promotions->tiers->redeem($promotionsTierId, $redemptionContext);
```

#### [Update Promotion's Tier]
```php
$client->promotions->tiers->update($promotionTierId);
```

#### [Delete Promotion's Tier]
```php
$client->promotions->tiers->delete($promotionTierId);
```

#### [List Available Promotion Tiers]
```php
$client->promotions->tiers->getAvailable();
```

---

### Async Actions API
Methods are provided within `$client->asyncActions->*` namespace.
- [Get Async Action](#get-async-action)
- [List Async Actions](#list-async-actions)

#### [Get Async Action]
```php
$client->asyncActions->get($id);
```
#### [List Async Actions]
```php
$client->asyncActions->getList();
$client->asyncActions->getList($params);
```

---

### Utils
To use utils you have to import Voucherify Utils class.

```php
require_once('vendor/autoload.php');

use Voucherify\Utils;
```
Available methods:

#### Verify Webhook Signature
```php
Utils::verifyWebhookSignature($signature, $message, $secretKey)
```

---

### Migration from 0.x

Version 1.x of the PHP is fully backward compatible with version 0.x.
Changes made in version 1.x mostly relate to grouping methods within namespaces.
So all you need to do is to follow the list bellow and just replace deprecated methods
with their namespaced equivalent.

#### Deprecated methods

- `$client->vouchers($params)` - [$client->vouchers->getList](#list-vouchers)
- `$client->get($code)` - [$client->vouchers->get](#get-voucher)
- `$client->create($voucher)` - [$client->vouchers->create](#create-voucher)
- `$client->update($voucher_update)` - [$client->vouchers->update](#update-voucher)
- `$client->delete($code, $force)` - [$client->vouchers->delete](#delete-voucher)
- `$client->disable($code)` - [$client->vouchers->disable](#disable-voucher)
- `$client->enable($code)` - [$client->vouchers->enable](#enable-voucher)
- `$client->redemption($code)` - [$client->redemptions->getForVoucher](#get-vouchers-redemptions)
- `$client->publish($campaign_name|$params)` - [$client->distributions->publish](#publish-voucher)
- `$client->redeem($code, $tracking_id|$params)` - [$client->redemptions->redeem](#redeem-voucher)
- `$client->redemptions($params)` - [$client->redemptions->getList](#list-redemptions)
- `$client->rollback($redemption_id, $params)` - [$client->redemptions->rollback](#rollback-redemption)
- `$client->customer->*` - changed namespace to [$client->customers->\*](#customers-api)

---
## Error handling

VoucherifyClient will throw custom `ClientException` object. To get sutructure described in our [API reference](https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#errors) please use:
```php
try {
    ...
}
catch (ClientException $e) {
    $error = $e->getError();
}
```

## Logging

VoucherifyClient has method `setLogger()` which can be used to set PSR-3 logger interface.

Set own logger if you want to preview curl request and response data.
```php
$logger = /* Initialaze logger i.e Monolog, Analog */

$client = new VoucherifyClient($apiID, $apiKey);
$client->setLogger($logger);
```

## Connection Options

Use `setConnectionOptions()` method to set client connection options.

Options:
- `timeout` - curl 'CURLOPT_TIMEOUT_MS'
- `connectTimeout` - curl 'CURLOPT_CONNECTTIMEOUT'

```php
$options = [
    "timeout" => 1500,
    "connectTimeout" => 2
];

$client = new VoucherifyClient($apiID, $apiKey);
$client->setConnectionOptions($options);
```

## Use case - CodeIgniter

Simple example of adding Voucherify to your CodeIgniter project.

### Setup

Download voucherify `/src` directory to `application/third_party/voucherify`.

### Custom Library

Create new library file in `/application/libraries` directory, i.e. `Coupons.php`.

```php
<?php defined('BASEPATH') OR exit('No direct script access allowed');

$src_voucherify = APPPATH . "third_party/voucherify/autoload.php";

include($src_voucherify);

use Voucherify\VoucherifyClient;
use Voucherify\ClientException;

class Coupons {

    public $voucherify;

    public function __construct() {
        $apiID  = "YOUR-APPLICATION-ID";
        $apiKey = "YOUR-CLIENT-SECRET-KEY";

        $this->voucherify = new VoucherifyClient($apiId, $apiKey);
    }
}
```

### Using Voucherify

Load new library and start using voucherify client.
```php
<?php defined('BASEPATH') OR exit('No direct script access allowed');

class Voucher extends CI_Controller {

    public function index()
    {
        $this->load->library('coupons');

        $voucherCode = "TEST-VOUCHER-CODE";
        $voucher = $this->coupons->voucherify->get($voucherCode);

        ...
    }
}
```

## Contributing

Bug reports and pull requests are welcome through [GitHub Issues](https://github.com/rspective/voucherify-php-sdk/issues).

### Changelog
- **2022-05-16** - `2.2.0` - Add CustomEvents support
- **2022-03-11** - `2.1.0` - Add AsyncActions support and a `$customHeaders` param
- **2019-07-19** - `2.0.0` - Hide API versioning in `$apiUrl` param
- **2018-12-28** - `1.7.10` - Add Validation Rule Assignments
- **2018-03-18** - `1.7.9` - Add Utils with verifyWebhookSignature method
- **2018-02-18** - `1.7.8` - Product delete force option support
- **2018-02-13** - `1.7.7` - Fix Promotions Tiers getAvailable method param
- **2018-02-13** - `1.7.6` - Promotions Tiers getAvailable method
- **2018-02-11** - `1.7.4` - Customers getList method
- **2018-01-14** - `1.7.3` - Promotions API
- **2017-07-24** - `1.7.2` - Fix get publications missing params
- **2017-07-23** - `1.7.1` - Api Client conneciton options
- **2017-07-12** - `1.7.0` - Orders API
- **2017-07-10** - `1.6.2` - PHP autoloading support
- **2017-07-07** - `1.6.1` - Remove Psr/Log dependency
- **2017-06-26** - `1.6.0` - Api Client logger support
- **2017-06-21** - `1.5.0` - Custom API URL support
- **2017-05-02** - `1.4.0` - API Version Header support
- **2017-05-02** - `1.3.0` - Validation rules API, Segments API, Products API
- **2017-04-27** - `1.2.0` - Validations API, Redemptions-Get, Distributions-Export
- **2017-04-26** - `1.1.0` - Campaigns API, Vouchers import method
- **2017-04-19** - `1.0.2` - Unit tests, bug fixes
- **2017-03-17** - `1.0.1` - Vouchers addBalance method
- **2017-02-19** - `1.0.0` - Namespace refectoring
- **2016-09-13** - `0.11.0` - Added new API method for voucher - publish
- **2016-09-13** - `0.10.0` - Added new API method for voucher - delete
- **2016-09-13** - `0.9.1` - Fix to maintain builder pattern.
- **2016-07-20** - `0.9.0` - Voucher code pattern.
- **2016-07-19** - `0.8.0` - Voucher update method.
- **2016-06-23** - `0.7.0` - Gift vouchers.
- **2016-04-27** - `0.6.0` - Added new API methods for customer - create, get, update, delete.
- **2016-04-27** - `0.5.0` - Rollback redemption.
- **2016-04-18** - `0.4.0` - List vouchers. Filter by customer.
- **2016-04-07** - `0.3.0` - List redemptions.
- **2016-04-04** - `0.2.2` - Updated API URL.
- **2016-03-03** - `0.2.1` - Fixed a typo (diasble -> disable).
- **2016-01-21** - `0.2.0` - Added new API methods - create, disable and enable.
- **2015-12-11** - `0.1.1` - New discount model. Added UNIT - a new discount type.
- **2015-12-02** - `0.1.0` - First version:
  - Authentication
  - Voucher informations: *get*, *redemption*
  - Voucher operations: *redeem*

[Get Async Action]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#get-async-actions-1
[List Async Actions]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#list-async-actions

[Create Voucher]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#create-voucher
[Get Voucher]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#vouchers-get
[Update Voucher]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#update-voucher
[Delete Voucher]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#delete-voucher
[List Vouchers]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#list-vouchers
[Enable Voucher]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#enable-voucher
[Disable Voucher]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#disable-voucher
[Add balance to Gift-Card Voucher]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#add-gift-voucher-balance
[Import Vouchers]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#import-vouchers-1

[Create Campaign]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#create-campaign
[Get Campaign]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq
[Add Voucher to Campaign]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#add-voucher-to-campaign
[Add Voucher with certain code to Campaign]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#add-voucher-with-certain-code-to-campaign
[Import Vouchers to Campaign]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#import-vouchers
[Delete Campaign]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#delete-campaign

[Publish Voucher]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#publish-voucher
[Create Export]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#create-export
[Get Export]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#get-export
[Delete Export]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#delete-export
[List Publications]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#list-publications

[Validate Voucher]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#validate-voucher
[Validate Promotion Campaign]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#validate-promotions-1

[Redeem Voucher]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#redeem-voucher
[Redeem Promotion's Tier]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#redeem-promotion
[Get Redemption]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#get-redemption
[List Redemptions]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#list-redemptions
[Get Voucher's Redemptions]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#vouchers-redemptions
[Rollback Redemption]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#rollback-redemption

[Create Customer]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#create-customer
[Get Customer]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#read-customer
[Update Customer]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#update-customer
[Delete Customer]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#delete-customer
[List Customers]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#list-customers

[Create Order]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#create-order
[Get Order]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#get-order
[Update Order]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#update-order
[List Orders]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#list-orders

[Create Product]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#create-product
[Get Product]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#get-product
[List Products]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#list-products
[Update Product]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#update-product
[Delete Product]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#delete-product

[Create SKU]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#create-sku
[Get SKU]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#get-sku
[List SKUs]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#list-skus
[Update SKU]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#update-sku
[Delete SKU]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#delete-sku

[Create Validation Rule]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#create-validation-rules
[Get Validation Rule]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#get-validation-rules
[List Validation Rules]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#list-validation-rules
[Update Validation Rule]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#update-validation-rules
[Delete Validation Rule]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#delete-validation-rules
[Create Validation Rule Assignment]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#create-validation-rules-assignment
[List Validation Rule Assignments]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#list-validation-rule-assignments
[Delete Validation Rule Assignment]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#delete-validation-rules-assignment

[Create Segment]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#create-segment
[Get Segment]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#get-segment
[Delete Segment]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#delete-segment

[Create Promotion Campaign]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#create-promotion-campaign
[Validate Promotion Campaign]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#validate-promotions-1
[List Promotion's Tiers]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#get-promotions
[Create Promotion's Tier]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#add-promotion-tier-to-campaign
[Redeem Promotion's Tier]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#redeem-promotion
[Update Promotion's Tier]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#update-promotion
[Delete Promotion's Tier]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#delete-promotion
[List Available Promotion Tiers]: https://docs.voucherify.io/reference?utm_source=github&utm_medium=sdk&utm_campaign=acq#introduction-1

[Track Custom Event]: https://docs.voucherify.io/reference/create-custom-event?utm_source=github&utm_medium=sdk&utm_campaign=acq