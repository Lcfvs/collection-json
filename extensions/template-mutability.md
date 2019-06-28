# Template Data Mutability

Support template data validation by adding optional `readonly` and `mutable` fields.

## The goals

1. To provide a way to specify if some fields are writable by the client (e.g. an API client) or not, inspired by the HTML `readonly` attribute
2. To know if the data may change or not, avoiding useless data exchanges.
3. To be able to create some static templates, where the state-based variations can be deduced by the service consumer, based on the entity state. 

## The fields

1. A `readonly` field (boolean, *default:* **false**), restricts the field mutability by the client, but not by the service provider.
2. A `mutable` field (boolean, *default:* **true**), restricts the field mutability, **once defined**, even by the client/provider.


```json
{ "collection" :
  {
    "version" : "1.0",
    "href" : "http://example.org/users",

    "template" : {
      "data" : [
        {"name" : "createdAt", "value" : "", "prompt" : "Creation time", "mutable": false, "readonly": true},
        {"name" : "modifiedAt", "value" : "", "prompt" : "Last modification time", "mutable": true, "readonly": true},
        {"name" : "username", "value" : "", "prompt" : "Login Name", "mutable": false, "readonly": false},
        {"name" : "email", "value" : "", "prompt" : "Email", "mutable": true, "readonly": false}
      ]
    }
  }
}
```

## Combinations meaning

```js
// writable by everyone, at any time
{ "readonly": false, "mutable": true}

// writable by everyone, once only
{ "readonly": false, "mutable": false}

// writable by the service provider, at any time
{ "readonly": true, "mutable": true}

// writable by the service provider, once only
{ "readonly": true, "mutable": false}
```

## template-validation +  template-mutability

[./template-validation.md](https://github.com/mamund/collection-json/blob/master/extensions/template-validation.md)

```js
// required at entity's creation, defined by everyone
{ "readonly": false, "required": true, "mutable": false}

// required at entity's creation, defined by the service provider
{ "readonly": true, "required": true, "mutable": false}
```

## References
1. https://groups.google.com/forum/#!topic/collectionjson/L2XpAdj-7DQ
