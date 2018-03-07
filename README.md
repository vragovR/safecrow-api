SafeCrow API v3
===============

A PHP wrapper to be used with SafeCrow API v3.

[![Build Status](https://travis-ci.org/vragovR/safecrow-api.svg?branch=master)](https://travis-ci.org/vragovR/safecrow-api)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/vragovR/safecrow-api/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/vragovR/safecrow-api/?branch=master)
[![Code Climate](https://codeclimate.com/github/vragovR/safecrow-api/badges/gpa.svg)](https://codeclimate.com/github/vragovR/safecrow-api)

Installation
------------

### 1: Download

```bash
$ composer require vragovr/safecrow-api "dev-master"
```

### 2: Configure

```php
$config = new \SafeCrow\Config('key', 'secret');

$client = new \SafeCrow\Client();

$client->authenticate($config);
```

### 3.1: Usage User Api

```php
# Add user
$user = $client->getUserApi()->add([
    'name' => 'Ivan Ivanov',
    'phone' => '79009996666',
    'email' => 'email@example.org',
]);

# Edit user
$user = $client->getUserApi()->edit([
    'name' => 'Ivan Ivanov',
    'phone' => '79009996666',
    'email' => 'email@example.org',
]);

# All users
$users = $client->getUserApi()->all();

# Show user
$user = $client->getUserApi()->show(1);

# All user orders
$orders = $client->getUserApi()->orders(1);

# Bind user card
$url = $client->getUserApi()->bind(1, [
    'callback_url' => 'https://example.org/success-card',
]);

# All users cards
$cards = $client->getUserApi()->cards([
    'all' => true,
]);
```

### 3.2: Usage Order Api
```php
# Add order
$order = $client->getOrderApi()->add([
    'consumer_id' => 1,
    'supplier_id' => 2,
    'price' => 10000,
    'description' => 'description...',
    'fee_payer' => Order::PAYER_HALF, // or Order::PAYER_CONSUMER or Order::PAYER_SUPPLIER
    'extra' => [],
]);

# All order
$orders = $client->getOrderApi()->all();

# Show order
$order = $client->getOrderApi()->show(1);

# Pay order
$url = $client->getOrderApi()->pay([
    'callback_url' => 'https://example.org/success-order',
]);

# Annul order
$order = $client->getOrderApi()->annul([
    'reason' => 'reason...',
]);

# Cancel order
$order = $client->getOrderApi()->cancel([
    'reason' => 'reason...',
    'method' => Order::METHOD_FULL, // or Order::METHOD_COMMISSION or Order::METHOD_PENALTY
]);

# Close order
$order = $client->getOrderApi()->close(1);

# Exception order
$order = $client->getOrderApi()->exception(1, [
    'reason' => 'reason...',
]);

# Bind card to order 
$order = $client->getOrderApi()->bind(1, 1, [
    'card_id' => 1,
]);
```

### 3.3: Usage Setting Api
```php
# Show setting
$setting = $client->getSettingApi()->show();

# Edit setting
$setting = $client->getSettingApi()->edit([
    'callback_url' => 'https://example.org/callback-order',
]);
```
