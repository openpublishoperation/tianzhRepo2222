# Support for REST API 

[Swagger](https://github.com/swagger-api/swagger-core/wiki) is a specification and complete framework implementation for describing, producing, consuming, and visualizing RESTful web services.

Support for Swagger 2.0 is integrated with OP. 

# Syntax

If you are using OA, you used to use the following syntax to invoke Swagger.

```RESTAPI_Swagger  
[!INCLUDE [users_swagger2](./users_swagger2.json)]  
```   

In Open Publishing, you should be using the following instead:

 `[!CODE-REST-i [users_swagger2](./users_swagger2.json)]`  
 
 Example:
 
 `[!CODE-REST-i [calendar_api_get_calendar_by_id](trydata/calendar_api_get_calendar_by_id.json)]`

Here's how it renders
```RESTAPIdocs
{
     "operation":    "get", 
     "showComponents": {        
        "codeGenerator": "true"
    } 
}
```
[!CODE-REST-i [calendar_api_get_calendar_by_id](trydata/calendar_api_get_calendar_by_id.json)]
