# trojan-caddy-docker-compose

[中文文档](https://github.com/qiushixiang/trojan-caddy-docker-compose/blob/master/README_CN.md)

Trojan server and Caddy integration with Docker compose。

Trojan server listens port 443. For https requests from normal sources, Trojan server will forward them to Caddy server for processing and return to the Web page while requests from Trojan client will be proxied by Trojan server which like V2ray+Websocket+TLS avoid GFW detection by disguising requests.

## quick start 
```
wget --no-check-certificate -O installation.sh https://github.com/qiushixiang/trojan-caddy-docker-compose/blob/master/installation.sh  && chmod +x installation.sh && sudo ./installation.sh
```

## or you want to deploy manually

Git clone this repo then change directory to this project.

1. Modify `./caddy/Caddyfile`:
    ```
    http://YOUR_DOMAIN_NAME {
    redir https://YOUR_DOMAIN.com{url}
	}

YOUR_DOMAIN_NAME:443 {
    log /usr/src/caddy.log
	}

:8080 {
    root /usr/src/trojan
    log /usr/src/caddy.log
    index index.html
	}
    ```
    Replace `YOUR_DOMAIN_NAME` with your own domain name.

2. Modify `./trojan/config/config.json`:

    Change `YOUR_PASSWORD` to your own password on `config:json:8` , this is your trojan password just safekeeping.
    
    Change `YOUR_DOMAIN_NAME` to your own domain name on `config:json:12-13`, this is your domain ssl certification path, Caddy server generate certs automatically on the path `/ssl/your_domain_name/your_domain_name.crt`
 
3. Run `docker-compose up` or `docker-compose up -d`  with Daemon mode
4. When each container is successfully built, it means that your Trojan and Caddy servers are working well.

## Tips

If you encounter any problems during the deployment process, you can raise them in' issue' considering various unknown situations.
