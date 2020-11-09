# Dockerfile-Openresty

This image enables the geoip function that doesn't be enabled in the official image by default.

## Description

The container image is built with the geoip function, so we can use this image as the official image with addtional feature. If you want to use more function of Openresty, you can fork this repository, add new build option and re-build the image by yourself.

This image is built without any entrypoint and command, it is very used as the base image to your application. You can contain your application with this image to a new image and write your own command to run the container.

## Run

### Docker

It recommends strongly that you use this image as the base image and package your own app and command to run the docker container.

### Docker Compose

You can use the `docker-compose.yml` file in the example folder to run the service and test easily. Even you can edit the `Dockerfile.openresty` to package your app to run what you want.

When you package your code into this image, even if you just want to mount your code into the container, there is some suggestion of the mounting point:
| Container Path                   | Usage                          |
| -------------------------------- | ------------------------------ |
| /usr/local/openresty/nginx/conf/ | Nginx or Openresty Config file |
| /usr/local/openresty/nginx/lua/  | Lua code Path                  |
| /var/www/                        | Static Web Page or Build Code  |

There is the example that you want to mount the config and code into the container with the `docker-compose.yml` file in the example folder, you just need to add the following code after `command` section
```
    volume: 
      ./conf:/usr/local/openresty/nginx/conf
      ./lua:/usr/local/openresty/nginx/lua
      ./app:/var/www
```

## Volume

No matter you want to package your code into this image or mount your code into the container, please put your code or config to each the following path 
- /usr/local/openresty/nginx/conf/
    The path to save the config of Nginx or Openresty. If you want to run your own settings or virtual host, you **must to** mount or add your config to this path, the Nginx or Openresty will include the config in this path by default.

- /usr/local/openresty/nginx/lua/
    The path to save the lua code by default. If you want to change this path, you need to specify in the config of Nginx or Openresty.

- /var/www/ 
    The path to save the app code by default. If you want to change this path, you need to specify in the config of Nginx or Openresty.

