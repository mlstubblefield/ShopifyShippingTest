I used
- https://shopify.dev/api/admin/rest/reference/shipping-and-fulfillment/carrierservice
- app.fakejson.com (doesn't pull from github, I load it in manually when I want to change it)

Here's a rough sketch on how to do it...
- Go to apps
- Create private app
- Accept stuff/name it
- Add permissions "Shipping - Read and Write"
- Crete App

https://shopify.dev/api/admin/rest/reference/shipping-and-fulfillment/carrierservice#create-2021-07
POST 
/admin/api/2021-07/carrier_services.json
DO NOT FORGET CONTENT TYPE application/json
{
  "carrier_service": {
    "name": "Speedway-Testo",
    "callback_url": "https://app.fakejson.com/q/98r5DtjP?token=zGcQ7HslrJzS1Rj6I_bZ0Q",
    "service_discovery": true
  }
}

When you create the app, it'll give you this URL with basic auth
https://XXXXX:XXXX@XXXX.myshopify.com/admin/api/2021-07/carrier_services.json

Once that's set up at some point you'll want to go in and delete the other/old rates (once it's deemed safe) (may want a back up plan) (probably use the api to do this?)
