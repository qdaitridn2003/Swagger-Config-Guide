# I. Definition

## 1. Swagger
```
    "swagger": "2.0",
    "info": {
        "title": "<title>",
        "description": "",
        "version": "<version>"
    },
    "securityDefinitions": {
        "bearerAuth": {
            "type": "apiKey",
            "name": "Authorization",
            "in": "header",
            "description": "Enter the token with the 'Bearer ' prefix, e.g. 'Bearer <JWT Token>'."
        }
    },
    "paths": {}
}
```
## 2. OpenApi
```
{
    "openapi": "3.1.1",
    "info": {
        "title": "<title>",
        "description": "",
        "version": "<version>"
    },
    "components": {
        "securitySchemes": {
            "bearerAuth": {
                "type": "http",
                "scheme": "bearer",
                "bearerFormat": "JWT"
            }
        }
    },
    "paths": {}
}
```
# II. Path Definition
## 1. Both (Swagger & OpenApi)
```
"<path>": {
    "<http-methods>": {
        "tags": "<tag>",
        "description": "<description>",
        "parameters": [<parameter>],
        "responses": {
            "200": {
                "description": "OK"
            }
        }
    }
}
```
## 2. With Bearer
### A. Swagger
```
"<path>": {
    "<http-methods>": {
        "tags": ["<tag>"],
        "description": "<description>",
        "parameters": [<parameter>],
        "security": [
            {
                "BearerAuth": []
            }
        ],
        "responses": {
            "200": {
                "description": "OK"
            }
        }
    }
}
```
### B. OpenApi
```
"<path>": {
    "<http-methods>": {
        "tags": ["<tag>"],
        "description": "<description>",
        "parameters": [<parameter>],
        "security": [
            {
                "bearerAuth": []
            }
        ],
        "responses": {
            "200": {
                "description": "OK"
            }
        }
    }
}
```
## 3. With Id
### A. Swagger
```
"<path/{id}>": {
    "<http-methods>": {
        "tags": ["<tag>"],
        "description": "<description>",
        "parameters": [
            {
                "in": "path",
                "name": "id",
                "type": "<type>",
                "example": "<example>", (optional)
                "description": "<description>" (optional)
                "required": <true | false> (optional)
            },
        ],
        "responses": {
            "200": {
                "description": "OK"
            }
        }
    }
}
```
### B. OpenApi
```
"<path/{id}>": {
    "<http-methods>": {
        "tags": ["<tag>"],
        "description": "<description>",
        "parameters": [
            {
                "in": "path",
                "name": "id",
                "schema": { "type": "<type>" },
                "example": "<example>", (optional)
                "description": "<description>", (optional)
                "required": <true | false> (optional)
            },
        ],
        "responses": {
            "200": {
                "description": "OK"
            }
        }
    }
}
```
## III. Parameters Definition
### A. Swagger
```
// FOR HEADER
{
    "in": "header",
    "name": "<name>",
    "type": "<type>",
    "example": "<example>", (optional)
    "description": "<description>", (optional)
    "required": <true | false> (optional)
},

// FOR PATH
{
    "in": "path",
    "name": "<name>",
    "type": "<type>",
    "example": "<example>", (optional)
    "description": "<description>", (optional)
    "required": <true | false> (optional)
}

# FOR QUERY
{
    "in": "query",
    "name": "<name>",
    "type": "<type>",
    "example": "<example>", (optional)
    "description": "<description>", (optional)
    "required": <true | false> (optional)
}

# FOR BODY
{
    "in": "body",
    "name": "<name>",
    "schema": {
        "type": "object",
        "required": ["<property>"]
        "properties": [
            { "<fieldName>": { "type" : "<type>" } }
        ]
    }
    "example": "<example>", (optional)
    "description": "<description>", (optional)
}

# FOR INPUT
{
    "in": "formData",
    "name": "<name>",
    "type": "<type>",
    "example": "<example>", (optional)
    "description": "<description>", (optional)
    "required": <true | false> (optional)
}

# FOR FILE
{
    "in": "formData",
    "name": "<name>",
    "type": "file",
    "example": "<example>", (optional)
    "description": "<description>", (optional)
    "required": <true | false> (optional)
}
```
### B. OpenApi
```
// FOR HEADER
{
    "in": "header",
    "name": "<name>",
    "schema": { "type": "<type>" },
    "example": "<example>", (optional)
    "description": "<description>", (optional)
    "required": <true | false> (optional)
},

// FOR PATH
{
    "in": "path",
    "name": "<name>",
    "schema": { "type": "<type>" },
    "example": "<example>", (optional)
    "description": "<description>", (optional)
    "required": <true | false> (optional)
}

# FOR QUERY
{
    "in": "query",
    "name": "<name>",
    "schema": { "type": "<type>" },
    "example": "<example>", (optional)
    "description": "<description>", (optional)
    "required": <true | false> (optional)
}

# FOR INPUT
{
    "in": "formData",
    "name": "<name>",
    "schema": { "type": "<type>" },
    "example": "<example>", (optional)
    "description": "<description>" (optional)
    "required": <true | false> (optional)
}
```
## IV. Bodies Definition (OpenApi)
```
// FOR DEFAULT
"requestBody": {
    "description" : "<description>", (optional)
    "required": <true | false>, (optional)
    "content": {
        "application/json": {
            "schema": {
                "type": "object",
                "properties": {
                    "<fieldName>": {
                        "type": "<type>",
                        "example": "<example>"
                    }
                }
            }
        }
    }
},


// FOR FILE
"requestBody": {
    "description" : "<description>", (optional)
    "required": <true | false>, (optional)
    "content": {
        "multipart/form-data": {
            "schema": {
                "type": "object",
                "properties": {
                    "<fieldName>": {
                        "type": "string",
                        "format": "binary"
                    }
                }
            }
        }
    }
},

// FOR BOTH OF THEM
"requestBody": {
    "description" : "<description>", (optional)
    "required": <true | false>, (optional)
    "content": {
        "multipart/form-data": {
            "schema": {
                "type": "object",
                "properties": {
                    "<fieldName>": {
                        "type": "string",
                        "format": "binary"
                    },
                    "<fieldName>": {
                        "type": "<type>",
                        "example": "<example>"
                    }
                }
            }
        }
    }
},
```
