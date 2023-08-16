{% info_block warningBox %}

Dynamic Multistore is part of an *Early Access Release*. This *Early Access* feature introduces the ability to handle the store entity in the Back Office. Business users can try creating stores without editing the `Stores.php` file and redeploying the system.

{% endinfo_block %}

This document describes how to install Dynamic Store + the Customer Account Management feature.

## Install feature core

### Prerequisites

Install the required features:

| NAME | VERSION |
| --- | --- |
| Spryker Core | {{page.version}} |
| Customer Account Management | {{page.version}} |


### Set up configuration

Add the following configuration to your project:

| CONFIGURATION | SPECIFICATION | NAMESPACE | COMMENTS |
| --- |----| --- |
| CustomerConfig::getCustomerSequenceNumberPrefix()| Provides a prefix used during customer reference generation. If no prefix provided it will use current store name that can lead to issues in Dynamic Store setup | Pyz\Zed\Customer | See in `src/Pyz/Zed/Customer/CustomerConfig.php` that follows. |


**src/Pyz/Zed/Customer/CustomerConfig.php**

```php
<?php

namespace Pyz\Zed\Customer;

use Spryker\Zed\Customer\CustomerConfig as SprykerCustomerConfig;

class CustomerConfig extends SprykerCustomerConfig
{
    /**
     * {@inheritDoc}
     *
     * @return string|null
     */
    public function getCustomerSequenceNumberPrefix(): ?string
    {
        return 'customer';
    }
}
```

{% info_block warningBox "Verification" %}

1. [Create a customer](/docs/pbc/all/customer-relationship-management/{{page.version}}/manage-in-the-back-office/customers/create-customers.html).
2. On the **Customers** page, next to the created customer, click **View**.
3. On the **View Customer** page, make sure that the **Customer Reference** contains the prefix you've configured.



{% endinfo_block %}
