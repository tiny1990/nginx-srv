# nginx upstream srv module

a nginx module, support dns srv base on tengine  `ngx_http_upstream_dynamic_module`

## How to support 
nginx `ngx_resolve_name` function query SRV record, if `ctx->service`  not empty.   
so `ngx_http_upstream_dynamic_module` set `ctx->service` is your domain suffix, `ctx->name` is servicename. 

## TODO
`ctx->service` read from upstream config

## config
like that
```config
    upstream backend {
        dynamic_resolve fallback=stale fail_timeout=30s;
        server test1.kns.local;
    }
```
expect config
```
    upstream backend {
        dynamic_resolve fallback=stale fail_timeout=30s;
        server kns.local test1;
    }
```
DNS SRV query: test1.kns.local
## Hard code current
https://github.com/tiny1990/nginx-srv/blob/master/ngx_http_upstream_dynamic_module.c#L512  
server name needs endWith `kns.local`


## What's the next
`ctx->name` and `ctx->serice` configable


