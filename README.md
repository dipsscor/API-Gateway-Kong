# API Gateway Kong with UI (Konga)
This project aims to showcase the various capabilities of Kong API Gateway and Konga (Additional UI for Kong). This project uses Postgres as DB for Kong and Kong configuration stores. 

There is a DB Less KONG configuration as well in next project.

## Kong
Kong is a widely adopted, open source API Gateway, written in Lua. It runs on top of Nginx, leveraging the OpenResty framework and provides a simple RESTful API that can be used to provision your infrastructure in a dynamic way.
Kong is referred to as microservices API Gateway.


### Kong is available in both community and Enterprise Edition:

![alt text](https://github.com/dipsscor/API-Gateway-Kong/blob/master/screenshots/version_comparision.png)

## Konga
Konga is a fully featured open source, multi-user GUI, that makes the hard task of managing multiple Kong installations a breeze.
It can be integrated with some of the most popular databases out of the box and provides the visual tools you need to better understand and maintain your architecture.



![alt text](https://github.com/dipsscor/API-Gateway-Kong/blob/master/screenshots/architecture.png)


# Setup - Configurations (Docker)


## Kong and Konga with Docker Compose

This Docker Compose template provisions a Kong container with a Postgres database, plus a nginx load-balancer. After running the template, the `nginx-lb` load-balancer will be the entrypoint to Kong.

To run this template execute:

    ```shell
    $ docker-compose up
    ```

To scale Kong (ie, to three instances) execute:

    ```shell
    $ docker-compose scale kong=3
    ```

Kong will be available through the `nginx-lb` instance on port `8000`, and `8001`. You can customize the template with your own environment variables or datastore configuration.

Kong's documentation can be found at [https://docs.konghq.com/][kong-docs-url].

The docker-compose template for Kong and Konga are available at:

    https://gist.github.com/pantsel/73d949774bd8e917bfd3d9745d71febf





## Kong and Konga without Docker-compose
Follow the instructions to provision Kong and Konga without docker-compose on:

    https://medium.com/@tselentispanagis/managing-microservices-and-apis-with-kong-and-konga-7d14568bb59d




# Feature - Configurations 

### Kong Admin API is available at : http://localhost:8001 
### Kong Gateway is avaliable at : http://localhost:8000

### Konga UI is avaliable at : http://localhost:1337



## Stage 1. Konga setup

    1. Browse to http://localhost:1337
    2. Create a admin user with username , email and password.
    3. Login to Konga
    4. Point to Kong connection :
            - Name : Any Name (e.g Kong)
            - URL : http://kong:8001/   ( since using docker-compose the Kong service is exposed to other containers as  "Kong" hostname)


## Stage 2. User setup

    1. Create some users in the user sections of Konga
    

## Stage 3. Services and Routes creation

For this POC, we’re going to use the excelent online fake API for testing and prototyping provided by "jsonplaceholder.typicode.com"


    1. Go to the Services section and create a new Service "Testing-Service"
    
          Config:
          
            - Protocol: "https" 
            
            - Host: "jsonplaceholder.typicode.com" ## For this POC we are using "jsonplaceholder.typicode.com" which provides some rest APIs.
            
            - Path: /API-V1.0  ## Path that would be used to get the endpoints : http://localhost:8000/API-V1.0/<route -path>
            
Note: Here Upstream server means the host and endpoint of the actual service.

    2. Go to routes section and create routes for following endpoints
            /users
            /comments
            /posts
            
            
          Config:   
            - Name: Give the name of the route
            
            - methods: Mention the HTTP methods ( GET, POST , PUT , PATCH , DELETE) in caps and press return. 
            
            - protocols: Select the protocols (HTTP,HTTPS) and press return.

Save the configurations and test the services at with all HTTP methods:

    http://locahost:8000/API-V1.0/users
    http://locahost:8000/API-V1.0/comments
    http://locahost:8000/API-V1.0/posts

The snapshot for service configuration can be found in snapshots --> service_route_configuration folder.



## Stage 4. Authentication - Basic

        1. Go the service created in Stage 3.
        2. Go to Plugins --> Add Plugin -->Authentication --> Basic Auth
        3. leave all fields and "add plugin"
        4. The Basic Auth plugin is created and applied to all "consumers" of the service with their usename/pwd.
        
        5. Go to "consumers" in left pane and create 2 consumers.
        
            - username: Give the username e.g. "mike , john" and submit
            - Create Basic credentials for the newly created consumers of the services
            - Credentials --> Basic Auth -->username: "mike/john"-->password--> "password"
            
        6. Go back to "services" section --> eligible consumers --> check both the consumers "mike /john" are added.
        
Test the services by passing the credentials in the header of the requests.

### Postman Logs:
    Without Authentication:
    
            GET http://localhost:8000/API-V1.0/comments

            {"message":"Unauthorized"}
            
    With Username and password:
    
            GET /API-V1.0/comments HTTP/1.1
            Authorization: Basic bWlrZTpwYXNzd29yZA==
            
            HTTP/1.1 200 OK



## Stage 5. Authentication - Key Auth

        1. Go the service created in Stage 3.
        2. Go to Plugins --> Add Plugin -->Authentication --> Key Auth
        3. Fill the form
            - key names : "apikey" ## Enter any key name that would be used as key name when adding to header
            - Key in body : Incase you want to supply key in body , enable this field
        4. The Key Auth plugin is created and applied to all "consumers" of the service with their api keys.
        
        5. Go to "consumers" in left pane and create 2 consumers.
        
            - username: Give the username e.g. "mike , john" and submit
            - Create Key Auth credentials for the newly created consumers of the services
            - Credentials--> API keys -->leave blank for Kong to generate the key.
            
        6. Go back to "services" section --> eligible consumers --> check both the consumers "mike /john" are added.
        
        
Test the services by passing the API key credential in the header of the requests.

### Postman logs:

    With incorrect keys:
    
            GET /API-V1.0/comments HTTP/1.1
            apikey: 1111

            {"message": "Invalid authentication credentials"}
            
    With correct keys:
    
            GET /API-V1.0/comments HTTP/1.1
            apikey: 2uASxFLd6bMc2qEgshr7qzvqzXVAZQ1A
            
            HTTP/1.1 200 OK



# References

    [kong-site-url]: https://konghq.com/
    [kong-docs-url]: https://docs.konghq.com/
    [github-new-issue]: https://github.com/Kong/docker-kong/issues/new
    https://medium.com/@tselentispanagis/managing-microservices-and-apis-with-kong-and-konga-7d14568bb59d
    https://gist.github.com/pantsel/73d949774bd8e917bfd3d9745d71febf
    https://docs.konghq.com/hub/
    
