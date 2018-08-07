    docker build -t visioncoder/centos7 .
docker build -t mailcatcher .
### Find the image id
     docker images
sudo docker run --rm=true -t -i -p 1080:1080 mailcatcher

### Add a new tag
    docker tag 4b7e3a58f21f visioncoder/centos7:latest



#docker build -t visioncoder/centos7:v1 .
#ID=$(docker build -t visioncoder/centos7 .) # This build and tag the image with creack/node:latest
#docker tag $ID /node:0.10.24  # Add a new tag
#docker tag $ID creack/node:latest   # You can use this and skip the -t part from build

#docker build --rm -t visioncoder/centos7 .
#ID=$(docker build -t visioncoder/centos7 .) # This build and tag the image with creack/node:latest
#docker tag $ID creack/node:0.10.24  # Add a new tag
#docker tag $ID creack/node:latest   # You can use this and skip the -t part from build

    docker build -t visioncoder/centos7test .