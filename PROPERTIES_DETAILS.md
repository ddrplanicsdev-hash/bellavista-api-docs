# Commercial Properties API

## Overview

Fetches commercial property details **properties-details**

---

## API URL

POST https://my3.optima-crm.com/v3/commercial_properties/view/726794?user=123

---

## Query Parameters

- `user` (required): Your user ID

---

## Example Request Body

```json
{
    "options": {
        "populate": [
            {
                "path": "property_attachments",
                "match": {
                    "document": {
                        "$ne": true
                    },
                    "publish_status": {
                        "$ne": false
                    }
                }
            }
        ]
    }
}
```
