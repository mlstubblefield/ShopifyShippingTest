I used
- https://shopify.dev/api/admin/rest/reference/shipping-and-fulfillment/carrierservice
- app.fakejson.com (doesn't pull from github, I load it in manually when I want to change it)

Here's a rough sketch on how to do it...
- Go to apps
- Create private app https://speedway-testo.myshopify.com/admin/apps/private
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
    "callback_url": "https://mlstest.vercel.app/api/shopify-shipping",
    "service_discovery": true
  }
}
you're probably going to update the provider eventually as well... when you need to do that, hit the PUT verison of the API with the same style of request body
https://speedway-testo.myshopify.com/admin/api/2021-07/carrier_services/58760659110.json

When you create the app, it'll give you this URL with basic auth
you can retrieve the URL by visiting the link to the private app and scrolling down...
https://speedway-testo.myshopify.com/admin/apps/private/333462831270
you'll need to modify it so that it points to the right API (like carrier_services)
https://XXXXX:XXXX@XXXX.myshopify.com/admin/api/2021-07/carrier_services.json

Once that's set up at some point you'll want to go in and delete the other/old rates (once it's deemed safe) (may want a back up plan) (probably use the api to do this?)
There's an option on the shipping dashboard to enable backup rates. Maybe that'd be good enough to add safety as we roll out.

To enable multiple shipping locations first go here
https://help.shopify.com/en/manual/locations/setting-up-your-locations
then follow these instructions
https://help.shopify.com/en/manual/shipping/setting-up-and-managing-your-shipping/convert-to-shipping-profile

Unknowns
- What if each warehouse returns different rates? Maybe I should make a fake vercel app to derisk this so I can put in some basic logic
- How do I show TNT expectations
- How can we do free shipping if I don't have the merch total for the entire order?
