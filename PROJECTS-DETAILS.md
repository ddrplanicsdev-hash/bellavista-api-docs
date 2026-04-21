# Projects details API

## Overview

Fetches project details info for the web page route **projects-details**

---

## API URL

GET or POST https://my3.optima-crm.com/yiiapp/frontend/web/index.php?r=constructions/view-by-ref&user=123&ref=5799&status[]=Available&model=commercial&similar_commercials=exclude_similar

---

## Query Parameters

- `user` (required): Your user ID

---

## How to get Quality report url for the "Documents of interest" section of the "projects-details" web page

Documents array path in json response :
- from `root -> documents`

Loop through documents and find document that has `identification_type` value as `QS`

Then extract below fields from the document object:
- `model_id`
- `file_md5_name`


Then create full document url using below `constructions_doc_url` value, `model_id` and `file_md5_name`:
```json
"constructions_doc_url" => "https://images.optima-crm.com/constructions_images",
```

Create full url as below:
- `constructions_doc_url/model_id/file_md5_name`

### PHP code snippet for above logic found in codebase:

```php
if (isset($property->documents) && count($property->documents) > 0) {
    foreach ($property->documents as $pic) {
        if (isset($pic->identification_type) && $pic->identification_type == 'QS') {
            if (isset(self::$constructions_doc_url))
                $quality_specifications[] = self::$constructions_doc_url . '/' . $pic->model_id . '/' . $pic->file_md5_name;
        }php code snippet for above logic
    }
    $return_data['quality_specifications'] = $quality_specifications;
}
```


## How to get sales file url for the "Documents of interest" section of the "projects-details" web page

Documents array path in json response :
- from `root -> documents`

Loop through documents and find document that has `identification_type` value as `128`

than extract below fields from document object:
- `model_id`
- `file_md5_name`

Then create full document url using below `constructions_doc_url` value, `model_id` and `file_md5_name`:
```json
"constructions_doc_url" => "https://images.optima-crm.com/constructions_images",
```

Create full url as below:
- `constructions_doc_url/model_id/file_md5_name`

### PHP code snippet for above logic found in codebase:

```php
if (isset($property->documents) && count($property->documents) > 0) {
    foreach ($property->documents as $pic) {
        if (isset($pic->identification_type) && $pic->identification_type == 128) {
            if (isset(self::$constructions_doc_url))
                $sales_dossier[] = self::$constructions_doc_url . '/' . $pic->model_id . '/' . $pic->file_md5_name;
        }
    }
    $return_data['sales_dossier'] = $sales_dossier;
}
```