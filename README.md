<img src="https://img.shields.io/github/license/GeniusGeeek/cors-bypass-proxy" /><a href="https://circleci.com/gh/badges/shields/tree/master">
  <img src="https://img.shields.io/circleci/project/github/badges/shields/master" alt="build status"></a>
  # cors-bypass-proxy
A PHP proxy to solve client browser HTTP CORS(cross-origin) restrictions.

A simple way to solve CORS issue when you have no access to the endpoint server is to have a proxy on your server, and this is just that, this may not take care of all security flaws but it does solve CORS issues.

## Installation
  PHP version: >= 7.x (recommended and tested)

Since ```proxy.php``` is indepedent and light, just simply upload it to your server

## Usage
Make a HTTP POST request to the proxy with your preferred framework/language, set headers required by the original endpoint if needed

```bash
  --Headers--
  example: Content-type: "appliciation/json"
  --data-body--
  example:
    {
        "cors": "http://example-api.com/endpoint", //endpoint URL
        "method": "POST", // should be the same with endpoint request type
        //endpoint data comes
        "param1": value, 
        "param2": value
    }
    
```
## usage with nativ JS and fethc

```javascript
var url = "myserver/proxy.php";
var params = {
    cors: "http://example-api.com/endpoint",
    method: "POST",
    param1: value1,
    param2: value2
};

fetch(url, {
    method: "POST",
    headers: {
        "Content-Type": "application/json"
    },
    body: JSON.stringify(params)
})
.then(function(response) {
    if (response.status === 200) {
        return response.json();
    } else {
        throw new Error("Anfrage fehlgeschlagen");
    }
})
.then(function(data) {
    console.log(data);
})
.catch(function(error) {
    console.error("Fehler: " + error.message);
});
```

 ## Usage with Jquery
 
 ```javascript
 $.ajax({
    url: "myserver/proxy.php",
    type: "POST", //endpoint request type
    crossDomain: true,
    //set request header here if needed by endpoint
    data: {
        "cors": "http://example-api.com/endpoint", //endpoint URL
        "method": "POST", // should be the same with endpoint request type
        //endpoint data comes
        "param1": value, 
        "param2": value
    },
    success: function (data) {
        console.log(data)
    }

});
 ```
 You can also send your request as stringified data like this if the API endpoint is compatible with it or receives request that way
 
 ```javascript
 $.ajax({
    url: "myserver/proxy.php",
    type: "POST", //endpoint request type
    crossDomain: true,
    //set request header here if needed by endpoint
    data: JSON.stringify({
        "cors": "http://example-api.com/endpoint", //endpoint URL
        "method": "POST", // should be the same with endpoint request type
        //endpoint data comes
        "param1": value, 
        "param2": value
    }),
    success: function (data) {
        console.log(data)
    }

});
 ```
 
 
 Now you have made a clean cross domain request
 
 ### Note
You can add headers specified by the api endpoint or server you are trying to access, request type valid for proxy are POST and GET methods only, method and cors parameter are compulsory fields for the proxy to work, Request type and method parameter should be the same and should be the valid method for the API/server endpoint.



