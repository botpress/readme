---
title: Integrations Actions
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
# Introduction

Integration actions in Botpress are the set of tasks that a chatbot can perform on a particular platform. This goes beyond the basic sending and receiving of messages. Actions offer a way for the bot to interact with various channels. For example, adding a reaction to a message on Slack, or starting a new conversation on Telegram. The exact way these actions are implemented will depend on the features provided by the external platform.

These actions are defined within the 'actions' object of your integration. They can then be called upon from your conversation flows in Botpress using the actions service.

We will be using our Botpress implementation for the Shopify [Retrieve a list of products](https://shopify.dev/docs/api/admin-rest/2023-01/resources/product#get-products?ids=632910392,921728736) as our examples.

> 📘 Action Concept
>
> You can find more about the [Actions Concept](../docs/actions) here.

<br />

# Action Definition

Each action is defined by several components: title, description, input, and output. The input and output schema are defined using the Zod library, which creates schemas for them. More information on Zod can be found here: [Zod Library](https://zod.dev/)

## Action Definition Parameters

In Botpress Integration Actions, each action is defined with a set of parameters: `title`, `description`, `input`, and `output`. 

### `title`

The `title` is a string that serves as the name of the action. It should be a short, concise name that describes what the action does. In our Shopify example, the title is "Get Products List", which is a brief, clear description of what the action does.

### `description`

The `description` is a string that provides more detailed information about what the action does. This will often include information on what the action is used for, any important notes about its usage, and any specific behavior it might have. In the Shopify example, the description "Gets a list of all products based on the parameters" tells the user that this action fetches a product list based on certain parameters.

### `input`

The `input` parameter is an object that defines the data that the action requires to run. It's made up of a `schema` and a `ui`:

* `schema`: This uses the Zod library to define the structure and type of the input data. In the Shopify example, it defines the fields `ids`, `limit`, `title`, and `product_type`, each of which have their own rules and descriptions.

* `ui`: This part of the input defines the user interface. It includes information that is helpful for the users when they are inputting data. For example, in the Shopify example, it gives a human-readable title and examples for each input field.

### `output`

The `output` parameter defines the data that the action will return. It's made up of a `schema`:

* `schema`: Just like the input schema, the output schema also uses the Zod library to define the structure and type of the output data. This defines what the data returned by the action will look like. In the Shopify example, the action returns an array of products in the `products_list`.

## Example of Action Definition:

The following example provides a definition for the 'Get Products List' action within a Shopify integration:

```ts
const getProducts = {
  title: "Get Products List",
  description: "Gets a list of all products based on the parameters",
  input: {
    schema: z.object({
      ids: z
        .string()
        .optional()
        .describe("Comma-separated list of product IDs."),
      limit: z
        .number()
        .min(0)
        .max(250)
        .default(50)
        .optional()
        .describe(
          "Return up to this many results per page. Default is 50, Maximum is 250"
        ),
      title: z.string().optional().describe("The exact product title."),
      product_type: z.string().optional().describe("Exact product type."),
    }),
    ui: {
      ids: {
        title: "Product ID(s)",
        examples: ["632910392", "632910392,632910391"],
      },
      limit: {
        title: "Limit",
      },
      title: {
        title: "Product Title",
      },
      product_type: {
        title: "Product Type",
      },
    },
  },
  output: {
    schema: z.object({
      products_list: z.array(z.object({}).passthrough()),
    }),
  },
};
```

<br />

# Action Implementation

After defining the action, you'll need to implement it in your integration. This involves writing the code that executes the action. The inputs for this code could include context (ctx), input data (from the fields defined in the UI section of the definition), a logger (to record information in the bot logs), and client (information about the integration).

## Action Implementation Parameters

The action implementation uses the parameters: `ctx`, `input`, `logger`, `client`:

### `ctx` (context)

The context contains information about the current state of the application or the user session. It includes configuration data like the shop name and the access token in our Shopify example.

### `input`

This is the data that the action requires to run, which is provided by the user. It's structured according to the `input` definition in the action definition. 

### `logger`

The logger allows you to record information in the bot logs. This is particularly useful for debugging, as you can log information about what the action is doing and any errors that might occur.

### `client` (not used in the provided example)

The client contains information about the integration and can be used to interact with the external service. For instance, if your action needs to send a request to an API, it would use the client to do so. In some cases, it might contain a pre-configured instance of an HTTP client or a client for a specific service.

## Example of Action Implementation:

The following example is an implementation of the 'Get Products List' action in a Shopify integration:

```ts
export const getProducts = async ({ ctx, input, logger }) => {
  const filters = await prepareParams(input);

  axios.defaults.baseURL = `https://${ctx.configuration.shopName}.myshopify.com`;
  axios.defaults.headers["X-Shopify-Access-Token"] = ctx.configuration.access_token;

  try {
    const response = await axios.get(
      `/admin/api/${SHOPIFY_API_VERSION}/products.json${
        filters.length > 0 ? "?" + filters : ""
      }`
    );
    
    const products_list = response.data.products;

    logger
      .forBot()
      .info(
        `Ran 'Get Products List' and found ${products_list.length} products matching criteria ${filters}`
      );

    return { products_list };
  } catch (e) {
    logger.forBot().debug(`'Get Products List' exception ${JSON.stringify(e)}`);
    return { products_list: {} };
  }
};
```

With the action defined and implemented, it can now be used within your chatbot's conversation flows. This action will reach out to Shopify, find a list of products that match the provided parameters, and return that list for the chatbot to use.
