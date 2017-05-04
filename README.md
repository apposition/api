# Apposition API documentation

Appostion API offers ability to report Shopify application install and uninstall events to Apposition service so that graphs in service offers detailed views of applications rank tracking.

## Requirments

- you need account on [Appostion](https://apposition.io)
- create application
- in application settings set application **Tracking Source** to **API**
- copy **App ID** and **App Secret**

## API

### Report application installs / uninstalls from Shopify Store

**Endpoint:** https://app.apposition.io/apprank/api/report

**HTTP Method:** POST

**JSON Body payload:**


    {
  
    "shopURL":"string, <*.myshopify.com>, Shopify URL",
    
    "status": "string, enum, possible values: installed, uninstalled",
    
    "timestamp": "long, optional, UTC timestamp in ms, timestamp of event, if not passed current timestamp is used"
    
    }
  
**Query parameters:**

- **id**: **App ID** recieved in Application settings
- **timestamp**: UTC current timestamp in ms, must be current time, server tolerate only 10 minutes delta based on current real time
- **hmac**: HMAC SHA-256 hex encoded signature of **signing payload** with secret **App secret**

**Signing payload:**

"**App ID** + **timestamp passed in query parameter** + **JSON body payload**"

For example if:
- App ID: "399"
- App Secret: "test"
- current timestamp: 1493901431000
- shop URL: "happy-customers.myshopify.com"
- status: "installed"
- timestamp of event: 1493901237000

Example payload: '3991493901431000{"shopURL":"happy-customers.myshopify.com","status":"installed","timestamp":1493901237000}'

Signature of payload: 'd3d1d6701d748dc9cc9153bc3e2388501e58d924eead9f4151850a82c5039ab3'

## Official SDKs:

- [NodeJS](https://www.npmjs.com/package/apposition)
