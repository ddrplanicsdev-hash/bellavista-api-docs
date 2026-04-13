# Commercial Properties API

## Overview
Fetches commercial property listings with filters like price, availability, and status.
Supports pagination, sorting, and relation loading. Used in page like **properties-for-sale**

---

## API URL

POST https://my3.optima-crm.com/v3/commercial_properties?user={user_id}

---

## Query Parameters

- `user` (required): Your user ID

---

## Example Request Body

```json
{
    "options": {
        "page": 1,
        "limit": 12,
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
        ],
        "sort": {
            "created_at": -1,
            "reference": 1
        }
    },
    "query": {
        "current_price": {
            "$gte": 600000,
            "$lte": 10000000000
        },
        "similar_commercials": "exclude_similar",
        "sale": true,
        "archived": {
            "$ne": true
        },
        "remove_count": true,
        "has_images": true,
        "status": {
            "$in": [
                "Available",
                "Under Offer"
            ]
        }
    }
}
```

## JavaScript Example

```js
fetch("https://my3.optima-crm.com/v3/commercial_properties?user=123", {
    method: "POST",
    body: JSON.stringify({
            "options": {
                "page": 1,
                "limit": 12,
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
                ],
                "sort": {
                    "created_at": -1,
                    "reference": 1
                }
            },
            "query": {
                "current_price": {
                    "$gte": 600000,
                    "$lte": 10000000000
                },
                "similar_commercials": "exclude_similar",
                "sale": true,
                "archived": {
                    "$ne": true
                },
                "remove_count": true,
                "has_images": true,
                "status": {
                    "$in": [
                        "Available",
                        "Under Offer"
                    ]
                }
            }
        }),
  })
  .then(res => res.json())
  .then(data => console.log(data));
```

## Notes

### Uses Mongo-style operators like `$gte`, `$lte`

Common Comparison Operators

  - `$eq` Matches values equal to a specified value.
  - `$gt` Matches values greater than a specified value.
  - `$gte` Matches values greater than or equal to a specified value.
  - `$in` Matches any values specified in an array.
  - `$lt` Matches values less than a specified value.
  - `$lte` Matches values less than or equal to a specified value.
  - `$ne` Matches all values not equal to a specified value.
  - `$nin` Matches if the value is not equal to any of a given list of values.

for more information about Mongo-style operators refer to https://www.mongodb.com/docs/manual/reference/mql/query-predicates/comparison/

# Sort properties query

```json
"options": {
    "sort": {
        "current_price": 1, #by price in ascending order
        "bedrooms":-1, #by bedrooms in descending order
        "created_at": 1,
        "reference": 1
    }
}
```

# Common filter query which goes under "query" object

### To filter properties by it's type like apartment, villa etc use below query block

```json
"type_one": {
    "$in": [
        136,
        150
    ]
}
```

### To filter properties by it's reference use below query block
```json
"$or": [
    {
        "reference": 726795
    },
    {
        "other_reference": {
            "$regex": ".*726795.*",
            "$options": "i"
        }
    },
    {
        "external_reference": {
            "$regex": ".*726795.*",
            "$options": "i"
        }
    }
]
```


### To filter properties by location use below query block
```json
"location": {
    "$in": [
        16,
        1415
    ]
}
```

### To filter properties based on price use below query block
```json
"current_price": {
    "$gte": 1000000,
    "$lte": 5000000
}
```

### To filter properties by bedrooms use below query block
```json
"bedrooms": {
    "$gte": 3
}
```

### To filter properties by status and get resale properties than use below query block
```json
"$and": [
    {
        "$or": [
            {
                "$and": [
                    {
                        "project": {
                            "$ne": true
                        }
                    },
                    {
                        "categories.new_construction": false
                    }
                ]
            },
            {
                "categories.resale": true
            }
        ]
    }
]
```

### To filter properties by status and get new development properties than use below query block
```json
"$and": [
    {
        "$or": [
            {
                "project": true
            },
            {
                "categories.new_construction": true
            }
        ]
    }
]
```

### To filter properties by views like sea, mountains, golf etc than use below query block
```json
"$and": [
    {
        "$or": [
            {
                "views.sea": true
            },
            {
                "views.mountain": true
            }
        ]
    },
    {
        "$or": [
            {
                "categories.golf": true
            },
            {
                "settings.close_to_golf": true
            },
            {
                "settings.frontline_golf": true
            },
            {
                "views.golf": true
            }
        ]
    }
]
```

### To filter properties by delivery date than use below query block
```json
"year_built": {
    "$exists": true,
    "$nin": [
        "",
        null
    ],
    "$lte": "2026-10-09"
}
```

### To filter properties by "distance to see" than use below query block
```json
"$and": [
    {
        "$or": [
            {
                "distances.sea.value": {
                    "$lte": 1
                },
                "distances.sea.unit": "km"
            },
            {
                "distances.sea.value": {
                    "$lte": 1000
                },
                "distances.sea.unit": "meters"
            }
        ]
    }
]
```
