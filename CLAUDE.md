# Vital Gmail

Gmail add-on for Vital Seeds that displays WooCommerce customer order history for the sender of the currently open email.

## Tech stack

- Google Apps Script (V8 runtime), deployed via [clasp](https://github.com/google/clasp)
- No build step — files are pushed directly with `clasp push`
- No npm, no bundler

## Project structure

```
project/
  appsscript.json   # Apps Script manifest (OAuth scopes, add-on config, URL whitelist)
  Code.js           # Card-building UI logic; Gmail add-on entry points
  DataRetrieval.js  # WooCommerce REST API calls
  ConfigHelpers.js  # Script Properties accessors
  Constants.js      # WooCommerce order status constants
```

## Configuration

All config is stored as Google Apps Script Properties (not env files). Required properties:

| Property | Notes |
|---|---|
| `WOOCOMMERCE_HOST` | Domain only, no protocol — e.g. `vitalseeds.co.uk` |
| `WOOCOMMERCE_CONSUMER_KEY` | Must start with `ck_` |
| `WOOCOMMERCE_CONSUMER_SECRET` | Must start with `cs_` |
| `REST_API_PREFIX` | Optional — defaults to `/wp-json` |
| `MAX_ORDER_COUNT` | Optional — defaults to `10` |

## Deployment

```bash
cd project
clasp push
```
