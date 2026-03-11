# NGINX URL Echo

This container is used to debug target URLs.  I was trying to create some redirect rules but need a way to have the path and query string answer with an OK instead of Not Found.


## Building the Container

To build the container and run it locally, run these commands:

```bash
docker build -t nginx-url-echo .
docker run --name nginx-url-echo -p 8080:80 nginx-url-echo
```

## Push to Azure Container Registry

For my use case, I needed this pushed to an Azure Container Registry.  To do this, run the following commands:

```bash
# login to your ACR
az acr login --name <container registry name without the azurecr.io>

# Tag your local image for the Azure Container Registry 
#   (where latest could be whatever tags you want to use)
docker tag nginx-url-echo:latest <container registry name>.azurecr.io/nginx-url-echo:latest

# Push the image to the container registry
#   (again using the tag from the previous step)
docker push <container registry name>.azurecr.io/nginx-url-echo:latest
```