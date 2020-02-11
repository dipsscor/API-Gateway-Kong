# API Gateway Kong with UI (Konga)
This project aims to showcase the various capabilities of Kong API Gateway and Konga (Additional UI for Kong). 

## Kong
Kong is a widely adopted, open source API Gateway, written in Lua. It runs on top of Nginx, leveraging the OpenResty framework and provides a simple RESTful API that can be used to provision your infrastructure in a dynamic way.
Kong is referred to as microservices API Gateway.

## Konga
Konga is a fully featured open source, multi-user GUI, that makes the hard task of managing multiple Kong installations a breeze.
It can be integrated with some of the most popular databases out of the box and provides the visual tools you need to better understand and maintain your architecture.



# Kong in Docker Compose

This is the official Docker Compose template for [Kong][kong-site-url].

# What is Kong?

You can find the official Docker distribution for Kong at [https://store.docker.com/images/kong](https://store.docker.com/images/kong).

# How to use this template

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

## Issues

If you have any problems with or questions about this image, please contact us through a [GitHub issue][github-new-issue].

## Contributing

You are invited to contribute new features, fixes, or updates, large or small; we are always thrilled to receive pull requests, and do our best to process them as fast as we can.

Before you start to code, we recommend discussing your plans through a [GitHub issue][github-new-issue], especially for more ambitious contributions. This gives other contributors a chance to point you in the right direction, give you feedback on your design, and help you find out if someone else is working on the same thing.

[kong-site-url]: https://konghq.com/
[kong-docs-url]: https://docs.konghq.com/
[github-new-issue]: https://github.com/Kong/docker-kong/issues/new