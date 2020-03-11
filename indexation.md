---
tags: [JsonApi]
---

# How to filter paginated list

## Filter by attributes

You can pass the **filter** param in order to filter the result set returned by the API. You can find below an example where the API will only return articles where the **title** is exactly **iPhone**.

```json
GET /articles
{
  "filter": {
    "title": "iPhone"
  }
}
```

It is possible to specify several filters for one request. In the below request, we are retrieving all articles where **title** is exactly **iPhone** and where the **price** is exactly **130**.

```json
GET /articles
{
  "filter": {
    "title": "iPhone",
    "price": 130
  }
}
```

### Use mathematical operators

In some cases, you might need to retrieve elements where an attribute is smaller or greater than a value, you can do that by using filter operators. The below request will retrieve you articles where **title** contains the word **iPhone** and where **price** is between **130** and **300**.

```json
GET /articles
{
  "filter": {
    "title": {
      "like": "%iPhone%"
    },
    "price": {
      ">": 130,
      "<": 300
    }
  }
}
```

### Use logical operators

You can use the OR operator in your filters, the below example will return all articles where **title** contains the word **iPhone** or where **price** is between **130** and **300**.

```json
GET /articles
{
  "filter": {
    "title": {
      "like": "%iPhone%"
    },
    "OR": {
      "price": {
        ">": 130,
        "<": 300
      }
    }
  }
}
```

### How to group filter

In more complex cases, you might need to group conditions together in order to reproduce the parenthesis priority system. Below is an example of filter grouping which will return articles where **comment** is exactly **broken glass** AND (**title** contains the word **iPhone** OR **price** is between **130** and **300**).

```json
GET /articles
{
  "filter": [
    {
      "comment": "broken glass"
    }, {
      "title": {
        "like": "%iPhone%"
      },
      "OR": {
        "price": {
          ">": 130,
          "<": 300
        }
      }
    }
  ]
}
```

## Filter by relationships

You can also filter results using resource relations, the below request will retrieve articles where the **author** is named **John Doe**.

```json
GET /articles
{
  "filter": {
    "author": {
      "name": "John Doe"
    }
  }
}
```

### Filter by relation ID

Filters can also be directly applied on relation ID. The below example will retrieve articles where the **author** ID is 42.

```json
GET /articles
{
  "filter": {
    "author": 42
  }
}
```