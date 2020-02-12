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



## 1. Konga setup

    1. Browse to http://localhost:1337
    2. Create a admin user with username , email and password.
    3. Login to Konga
    4. Point to Kong connection :
            - Name : Any Name (e.g Kong)
            - URL : http://kong:8001/   ( since using docker-compose the Kong service is exposed to other containers as  "Kong" hostname)


# References

    [kong-site-url]: https://konghq.com/
    [kong-docs-url]: https://docs.konghq.com/
    [github-new-issue]: https://github.com/Kong/docker-kong/issues/new
    https://medium.com/@tselentispanagis/managing-microservices-and-apis-with-kong-and-konga-7d14568bb59d
    https://gist.github.com/pantsel/73d949774bd8e917bfd3d9745d71febf
    https://docs.konghq.com/hub/
    
