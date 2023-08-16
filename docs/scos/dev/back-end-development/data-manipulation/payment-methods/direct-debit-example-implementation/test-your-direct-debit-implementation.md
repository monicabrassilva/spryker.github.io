---
title: Test your Direct Debit implementation
description: This document describes how to test the direct debit payment implementation.
last_updated: Jun 16, 2021
template: howto-guide-template
originalLink: https://documentation.spryker.com/2021080/docs/dd-test-implementation
originalArticleId: 99869c48-6a06-42b7-a110-d06efad2fcd5
redirect_from:
  - /2021080/docs/dd-test-implementation
  - /2021080/docs/en/dd-test-implementation
  - /docs/dd-test-implementation
  - /docs/en/dd-test-implementation
  - /v6/docs/dd-test-implementation
  - /v6/docs/en/dd-test-implementation
  - /v5/docs/dd-test-implementation
  - /v5/docs/en/dd-test-implementation
  - /v4/docs/dd-test-implementation
  - /v4/docs/en/dd-test-implementation
  - /v3/docs/dd-test-implementation
  - /v3/docs/en/dd-test-implementation
  - /v2/docs/dd-test-implementation
  - /v2/docs/en/dd-test-implementation
  - /v1/docs/dd-test-implementation
  - /v1/docs/en/dd-test-implementation
  - /docs/scos/dev/back-end-development/data-manipulation/payment-methods/direct-debit-example-implementation/testing-your-direct-debit-implementation.html
related:
  - title: Implement Direct Debit payment
    link: docs/scos/dev/back-end-development/data-manipulation/payment-methods/direct-debit-example-implementation/implement-direct-debit-payment.html
  - title: Implement Direct Debit in Yves
    link: docs/scos/dev/back-end-development/data-manipulation/payment-methods/direct-debit-example-implementation/implement-direct-debit-in-yves.html
  - title: Implement Direct Debit in Zed
    link: docs/scos/dev/back-end-development/data-manipulation/payment-methods/direct-debit-example-implementation/implement-direct-debit-in-zed.html
  - title: Implement Direct Debit in the shared layer
    link: docs/scos/dev/back-end-development/data-manipulation/payment-methods/direct-debit-example-implementation/implement-direct-debit-in-the-shared-layer.html
  - title: Integrate Direct Debit into checkout
    link: docs/scos/dev/back-end-development/data-manipulation/payment-methods/direct-debit-example-implementation/integrate-direct-debit-into-checkout.html
---

After the Direct Debit payment method has been set up on the [frontend](/docs/scos/dev/back-end-development/data-manipulation/payment-methods/direct-debit-example-implementation/implement-direct-debit-in-yves.html), [backend](/docs/scos/dev/back-end-development/data-manipulation/payment-methods/direct-debit-example-implementation/implement-direct-debit-in-zed.html), and [shared implementation](/docs/scos/dev/back-end-development/data-manipulation/payment-methods/direct-debit-example-implementation/implement-direct-debit-in-the-shared-layer.html), test it by [submitting a new order](/docs/scos/user/features/{{site.version}}/checkout-feature-overview/multi-step-checkout-overview.html) from Yves. Then, you can manage the flow of the order [in the Back Office](/docs/pbc/all/order-management-system/{{site.version}}/base-shop/manage-in-the-back-office/orders/change-the-state-of-order-items.html).
