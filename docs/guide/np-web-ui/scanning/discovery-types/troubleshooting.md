# 👾 Troubleshooting 

This section provides the guidelines on how to deal with a parsing error which may occur while uploading an API schema for a new scan.

### OpenAPI/Swagger Schema Validation Checklist

If you get a parsing error when uploading an OpenAPI schema to Nexploit, validate and correct the schema configuration according to the following checklist: 

1. The target **server (host)** is specified:
    * If you are using OpenAPI  3+,  include the `servers` variable.
    * If you are using a Swagger 2+ schema, include the `host` variable.

2. The **path parameters start with `/`**, for example `/home`.
3. A **substitution for the** `server` **and** `path` **variables** is provided.  If no substitution is used, Nexploit automatically defines the data type and generates a random alternate value when parsing the schema. By specifying the substitutions, you ensure correct and complete scan results. 

    Here is an example of substitution with the default value, description, and enumeration of strings (taken from the [Swagger documentation](https://swagger.io/specification/):

```
{
  "servers": [
    {
      "url": "https://{username}.gigantic-server.com:{port}/{basePath}",
      "description": "The production API server",
      "variables": {
        "username": {
          "default": "demo",
          "description": "this value is assigned by the service provider, in this example `gigantic-server.com`"
        },
        "port": {
          "enum": [
            "8443",
            "443"
          ],
          "default": "8443"
        },
        "basePath": {
          "default": "v2"
        }
      }
    }
  ]
}
```

For JSON schemas, you can also use the properties to define the input and output data types, for example, `minimum`, `maximum`, `multipleOf`, etc. For more information about possible substitutions, see [Swagger documentation](https://swagger.io/specification/),  [JSON Schema Core](https://tools.ietf.org/html/draft-wright-json-schema-00) and [JSON Schema Validation](https://tools.ietf.org/html/draft-wright-json-schema-validation-00). 


### Postman Schema Validation Checklist
If you get a parsing error when uploading a Postman collection to Nexploit, validate and correct the schema configuration according to the following checklist: 

1. The `URL` item is specified properly, for example: 
    * Literal

    ```
    {{url}}/.well-known/openid-configuration?client_id={{clientId}}
    ```

    * Broken-down
```
    "url": {
    "raw": "{{url}}/.well-known/openid-configuration?client_id={{clientId}}",
    "host": [
    "{{url}}"
    ],
    "path": [
    ".well-known",
    "openid-configuration"
    ],
    "query": [
    {
    "key": "client_id",
    "value": "{{clientId}}"
    }
    ]
    }
```
A problem may arise when the structure of a broken-down URL is incorrect, or the required (expected) fields are missing. Please refer to the [Postman documentation](https://schema.postman.com/) for more information.

    Here is an example of incomplete URL:

    ```
    "url": { 
    "raw": "{{url}}/.well-known/openid-configuration?client_id={{clientId}}"
    }
    ```

2. Every  environmental variable has a substitution value. If no substitution is used, Nexploit automatically detects the data type and generates a random alternate value when parsing the schema.  By specifying the substitutions, you ensure correct and complete scan results. 



