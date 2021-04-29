# Configuring an API Schema for Scanning
To scan API endpoints, you need to upload the relevant schema file to Nexploit. For a scan to be successful, please make sure that you use a valid schema which is configured in compliance with the original specification ([OpenAPI/ Swagger](https://swagger.io/specification/) or [Postman](https://schema.postman.com/) respectively). 

Nexploit parses the uploaded file to define the surface of the scanned target. If the schema is configured incorrectly (breaks the specification rules), Nexploit cannot accept the file and displays an error message.

Before uploading an API schema to Nexploit, we recommend that you validate it using one of the standard tools that check for the RFC.

The examples of API schemas that can be properly defined by Nexploit are given below.

<!-- tabs:start -->

##### **Swagger.json**

```bash
{
 "swagger": "2.0",
 "info": {
   "title": "schema",
   "description": "My API Schema",
   "version": "0.4.5"
 },
 "host": "brokencrystals.com",
 "basePath": "/home",
 "schemes": [
   "https"
 ],
 "paths": {
   "/user/{userEmail}": {
     "get": {
       "parameters": [
         {
           "in": "path",
           "name": "userEmail",
           "required": true,
           "type": "string",
           "default": "docs@neuralegion.com"
         }
       ],
       "produces": [
         "application/json"
       ],
       "responses": {
         "200": {
           "description": "OK"
         }
       }
     }
   }
 }
}

```

##### **Swagger.yaml**
```bash
swagger: "2.0"
info:
 title: schema
 description: My API Schema
 version: 0.4.5
host: brokencrystals.com
basePath: /home
schemes:
 - https
paths:
 /user/{userEmail}:
   get:
     parameters:
     - in: path
       name: userEmail
       required: true
       type: "string"
       default: "docs@neuralegion.com"
     produces:
       - application/json
     responses:
       200:
         description: OK

```

##### ** OpenAPI.json**

```bash
{
 "openapi": "3.0.1",
 "info": {
   "title": "schema",
   "description": "My API Schema",
   "version": "0.4.5"
 },
 "servers": [
   {
     "url": "https://brokencrystals.com/{basePath}",
     "variables": {
       "basePath": {
         "default": "/home"
       }
     }
   }
 ],
 "paths": {
   "/user/{userEmail}": {
     "post": {
       "operationId": "userEmail",
       "parameters": [
         {
           "name": "userEmail",
           "in": "path",
           "required": true,
           "schema": {
             "type": "string",
             "default": "docs@neuralegion.com"
           }
         }
       ],
       "responses": {
         "200": {
           "description": "200 response",
           "content": {
             "application/json": {
               "schema": {
                 "$ref": "#"
               }
             }
           }
         }
       }
     }
   }
 }
}

```

##### **OpenAPI.yaml**

```bash
openapi: "3.0.1"
info:
 title: "schema"
 description: "My API Schema"
 version: "0.4.5"
servers:
- url: "https://brokencrystals.com/{basePath}"
 variables:
   basePath:
     default: "/home"
paths:
 /user/{userEmail}:
   post:
     operationId: "userEmail"
     parameters:
     - name: "userEmail"
       in: "path"
       required: true
       schema:
         type: "string"
         default: "docs@neuralegion.com"
     responses:
       "200":
         description: "200 response"
         content:
           application/json:
             schema:
               $ref: "#"

```


##### **Postman**
```bash
{
  "info": {
     "name": "schema",
     "description": "My API Schema",
     "schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
  },
  "item": [
     {
        "name": "/user/:userEmail",
        "request": {
           "method": "GET",
           "header": [],
           "url": {
              "raw": "{{baseUrl}}/user/:userEmail",
              "host": [
                 "{{baseUrl}}"
              ],
              "path": [
                 "user",
                 ":userEmail"
              ],
              "variable": [
                 {
                    "key": "userEmail",
                    "value": "docs@neuralegion.com",
                    "description": "(Required) "
                 }
              ]
           }
        },
        "response": [
           {
              "name": "OK",
              "originalRequest": {
                 "method": "GET",
                 "header": [],
                 "url": {
                    "raw": "{{baseUrl}}/user/:userEmail",
                    "host": [
                       "{{baseUrl}}"
                    ],
                    "path": [
                       "user",
                       ":userEmail"
                    ],
                    "variable": [
                       {
                          "key": "userEmail"
                       }
                    ]
                 }
              },
              "status": "OK",
              "code": 200,
              "header": [
                 {
                    "key": "Content-Type",
                    "value": "text/plain"
                 }
              ],
              "cookie": [],
              "body": ""
           }
        ]
     }
  ],
  "variable": [
     {
        "key": "baseUrl",
        "value": "https://brokencrystals.com/home",
        "type": "string"
     }
  ]
}
 

```

<!-- tabs:end -->