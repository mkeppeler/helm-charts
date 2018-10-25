# Welcome to my chart repo

![Node-RED](https://nodered.org/about/resources/media/node-red-icon.png=50x50)

## Content

- Creating the Node-RED Image and upload it to IBM Cloud Private

## Creating the Node-RED Image and upload it to IBM Cloud Private

You need a linux environment with docker installed.

1. From a command line run the following command to pull and start the container
```
docker run -it -p 1880:1880 --name mynodered nodered/node-red-docker
```
For more information about this command, go to https://hub.docker.com/r/nodered/node-red-docker/

2. If you open localhost:1880 you will be in the Node Red console. To install other nodes, like watson, in Node-RED run
```
docker exec -it mynodered /bin/bash
```
3. Now your running the command line in your container, run `npm install`  to add the watson package.
```
npm install node-red-node-watson
```
Once you installed the package you want restart the container
```
docker stop mynodered
docker start mynodered
```
4. To create a new image from the container run
```
docker commit mynodered node-red-watson
```
5. Run your new image to make sure the changes have made it into the new images
```
docker run -d --restart=always -p 1880:1880 node-red-watson:latest
```
6. Tag the image and upload it to your IBM Cloud Private instance by executing
```
docker tag node-red-watson:latest mycluster.icp:8500/default/node-red-watson:0.19.04
docker login mycluster.icp:8500
docker push mycluster.icp:8500/default/node-red-watson:0.19.04
```
Also see [pushung and pulling images](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_3.1.0/manage_images/using_docker_cli.html) [add a helm chart to the internal repo](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_3.1.0/app_center/add_package.html#add_internal)


For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).
