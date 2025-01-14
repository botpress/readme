---
title: Register & Unregister
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Register

`register` is fired when the integration is enabled. It's essential to note that `register` is idempotent and can be triggered multiple times, so it's crucial to ensure that your integration handles this appropriately. 

`register` is the perfect place to create webhooks or subscribe the Botpress webhook to the integration to receive information. It is also a suitable place to verify the correctness of the information provided in the configuration.

Here's an example of `register` in a Shopify integration:

```javascript
import axios from 'axios'
import type * as botpress from '.botpress'
import { SHOPIFY_API_VERSION } from '../const'

type Implementation = ConstructorParameters<typeof botpress.Integration>[0]
type RegisterFunction = Implementation['register']

export const register: RegisterFunction = async ({ client, ctx, logger, webhookUrl }) => {
  axios.defaults.baseURL = `https://${ctx.configuration.shopName}.myshopify.com`
  axios.defaults.headers['X-Shopify-Access-Token'] = ctx.configuration.access_token
  axios.defaults.headers['Content-Type'] = 'application/json'

  
  try {
    let response = await axios.get(
      `/admin/api/${SHOPIFY_API_VERSION}/webhooks.json?topic=orders/create&address=${webhookUrl}`
    )

    if(response.data.webhooks.length > 0)
    {
      logger
      .forBot()
      .info(`Shopify New Order Webhook was found with id ${response.data.webhooks[0].id.toString()} for Bot ${ctx.botId}. Webhook was not created`)

      return
    }    

    response = await axios.post(`/admin/api/${SHOPIFY_API_VERSION}/webhooks.json`, {
      webhook: {
        topic: 'orders/create',
        address: webhookUrl,
        format: 'json',
      },
    })

    await client.setState({
      type: 'integration',
      name: 'configuration',
      id: ctx.integrationId,
      payload: { webhookId: response.data.webhook.id.toString() },
    })

    logger
      .forBot()
      .info(`Shopify New Order Webhook Created ${response.data.webhook.id.toString()} for Bot with Id ${ctx.botId}`)
  } catch (e) {
    logger.forBot().error(`'Shopify New Order Webhook Creation' exception ${JSON.stringify(e)}`)
  }
}
```

# Unregister

`unregister` is called when the integration is deleted from the bot. This is the best place to delete the webhooks, events, triggers, etc., that you created in the `register` function.

Here's an example of `unregister` in a Shopify integration:

```javascript
import axios from 'axios'
import type * as botpress from '.botpress'
import { SHOPIFY_API_VERSION } from '../const'

type Implementation = ConstructorParameters<typeof botpress.Integration>[0]
type UnregisterFunction = Implementation['unregister']

export const unregister: UnregisterFunction = async ({ ctx, client, logger }) => {

  axios.defaults.baseURL = `https://${ctx.configuration.shopName}.myshopify.com`
  axios.defaults.headers['X-Shopify-Access-Token'] = ctx.configuration.access_token
  axios.defaults.headers['Content-Type'] = 'application/json'

  // your code continues here...
}
```

Make sure to properly handle all possible exceptions and log them using the provided `logger`.
