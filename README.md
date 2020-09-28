# vostro/cloudflare-railgun
Dockerfile for cloudflare's railgun

## Introduction
Railgun ensures that the connection between your origin server and the Cloudflare network is as fast as possible.

Railgun compresses previously uncacheable web objects up to 99.6% by leveraging techniques similar to those used in the compression of high-quality video. This results in an average 200% additional performance increase.

https://www.cloudflare.com/website-optimization/railgun/

## Deployment

### Containers
 - memcached:latest : memcached

### Ports
 - 2408/TCP

### Environment Variables
 - RG_ACT_TOKEN         Token from Cloudflare Portal
 - RG_ACT_HOST          External IP address of Host
 - RG_LOG_LEVEL         Logging Level : default: 0
 - RG_WAN_PORT          External Port : default: 2408
 - RG_MEMCACHED_SERVERS Memcached server(s) : default : linked memcached container
 
### Command Line
 ``` 
 docker run --name railgun-memcached -d --restart=always memcached:latest
 
 docker run -d --name=railgun -p 2408:2408 -e RG_ACT_TOKEN=ENTERTOKENHERE \
 -e RG_ACT_HOST=192.0.2.1 \
 -e RG_LOG_LEVEL=1 \
 -e RG_WAN_PORT=2408 \
 --link railgun-memcached:memcached \
 --restart=always \
 vostro/cloudflare-railgun
 ```
