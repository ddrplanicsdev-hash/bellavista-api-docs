# 🏗️ Constructions API Documentation

## Overview
Fetches project details list. Used in page like **search-for-projects**

## 📌 Base URL

```
https://my3.optima-crm.com/yiiapp/frontend/web/index.php?r=constructions
```

---

## 🔑 Required Parameters

| Parameter   | Type    | Description                            |
| ----------- | ------- | -------------------------------------- |
| `user`      | integer | User ID (provided by system)           |
| `page`      | integer | Pagination page number (starts from 0) |
| `page_size` | integer | Number of results per page             |

---

## 📊 Example Request

```
https://my3.optima-crm.com/yiiapp/frontend/web/index.php?r=constructions&user=123&page=0&page_size=12&orderby[]=created_at&orderby[]=DESC&orderby[]=updated_at&orderby[]=DESC&prop_phase_wise=true&phase_low_price_from=600000&phase_heigh_price_from=100000000&has_images=true
```

---

## 🔍 Filtering Parameters

### 📍 Location Filters

| Parameter            | Type  | Example                       |
| -------------------- | ----- | ----------------------------- |
| `address_province[]` | array | `address_province[]=Alicante` |
| `location[]`         | array | `location[]=Beach`            |
| `city[]`             | array | `city[]=Valencia`             |
| `location_group[]`   | array | `location_group[]=coastal`    |

---

### 🏠 Property Details

| Parameter      | Type   | Description                 |
| -------------- | ------ | --------------------------- |
| `type[]`       | array  | Property types              |
| `categories[]` | array  | Property categories         |
| `reference`    | string | Specific property reference |

---

### 🛏️ Rooms

| Parameter     | Type  | Example                        |
| ------------- | ----- | ------------------------------ |
| `bedrooms[]`  | array | `bedrooms[]=2&bedrooms[]=50`   |
| `bathrooms[]` | array | `bathrooms[]=1&bathrooms[]=50` |

#### Range Format (Alternative)

| Parameter        | Example |
| ---------------- | ------- |
| `bedrooms`       | `2,50`  |
| `bathrooms_from` | `1`     |
| `bathrooms_to`   | `50`    |

---

### 💰 Price Filters

| Parameter                | Description   |
| ------------------------ | ------------- |
| `phase_low_price_from`   | Minimum price |
| `phase_heigh_price_from` | Maximum price |

#### Example

```
&phase_low_price_from=600000
&phase_heigh_price_from=100000000
```

---

### 📏 Size Filters

| Parameter         | Description        |
| ----------------- | ------------------ |
| `built_size_from` | Minimum built area |
| `built_size_to`   | Maximum built area |
| `usefull_area`    | Useful area        |

---

### 🧭 Orientation & Features

| Parameter            | Type  |
| -------------------- | ----- |
| `orientation[]`      | array |
| `features[]`         | array |
| `general_features[]` | array |
| `views[]`            | array |

---

### 🌴 Amenities

| Parameter    | Example                |
| ------------ | ---------------------- |
| `pool[]`     | `pool[]=pool_communal` |
| `garden[]`   | `garden[]=private`     |
| `parking[]`  | `parking[]=garage`     |
| `leisures[]` | `leisures[]=golf`      |

---

### 🆕 Special Filters

| Parameter                  | Description                 |
| -------------------------- | --------------------------- |
| `conditions[]=never_lived` | New property                |
| `pool[]=pool_communal`     | Communal pool               |
| `has_images=true`          | Only properties with images |

---

### 📅 Additional Filters

| Parameter          | Example                 |
| ------------------ | ----------------------- |
| `phase_built_year` | `1970-01-01,2020`       |
| `distances_sea`    | `5,km` or `5000,meters` |

---

### 🔀 Sorting

| Parameter   | Example                               |
| ----------- | ------------------------------------- |
| `orderby[]` | `orderby[]=created_at&orderby[]=DESC` |

You can apply multiple sorting rules:

```
orderby[]=created_at&orderby[]=DESC
orderby[]=updated_at&orderby[]=DESC
```

---

## 📄 Pagination

| Parameter   | Example |
| ----------- | ------- |
| `page`      | `0`     |
| `page_size` | `12`    |

---

## 🧪 JavaScript Example

```javascript
const url = new URL("https://my3.optima-crm.com/yiiapp/frontend/web/index.php");

url.search = new URLSearchParams({
  r: "constructions",
  user: 123,
  page: 0,
  page_size: 12,
  "phase_low_price_from": 600000,
  "phase_heigh_price_from": 100000000,
  "has_images": true
});

fetch(url)
  .then(res => res.json())
  .then(data => console.log(data));
```

---

## 🧪 cURL Example

```bash
curl "https://my3.optima-crm.com/yiiapp/frontend/web/index.php?r=constructions&user=123&page=0&page_size=12"
```

---

## ⚠️ Notes

* Array parameters use `[]` format
* Empty values are ignored
* Some filters depend on backend configuration
* Max values (like `50` for bedrooms) are used as upper limits
* `has_images=true` ensures only listings with images are returned

---

## ✅ Best Practice

* Always send only required filters
* Avoid sending empty parameters
* Use pagination for performance
* Combine filters for precise results

---

## 🚀 Summary

This API allows you to:

* Filter properties by location, price, size, and features
* Sort and paginate results
* Retrieve only relevant listings (e.g., with images)

---
