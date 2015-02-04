---
layout: post
title:  “Docker containers stored in Dogestry”
date:   2015-02-03 12:00:00
categories: docker, dogestry
---
Once you play with Docker it comes the time when you need to store docker images. There are public docker registries. There are private docker registries for money, too. You can host docker registry service too.

However, there is one very cheap option. It’s S3. Even though S3 is strongly supported by Docker Registry service you can skip the service layer and push/pull container images directly to S3.

For that there is dogestry project: https://github.com/dogestry/dogestry

There were lack of instructions. Therefor, here are my snippets how I made it work.

1. Checkout repository inside your host machine where you have Docker already runing.
2. To install: `./build.sh`. The outcome is that you have built docker named ‘dogestry’. It contains dogestry executable that can push/pull containers to S3.
3. Run `dogestry` inside `dogestry` container:  

```bash
sudo docker run --rm -e "AWS_ACCESS_KEY=" -e "AWS_SECRET_KEY=" -v /var/run/docker.sock:/var/run/docker.sock dogestry dogestry push s3:///aws-s3-bucket-name/folder name-of-your-pushed-container
```

- sudo or no-sudo. It depends on you how you make it work  
- `run --rm` drop the container that has been built after the task  
- `-e "AWS..."` pass AWS S3 credentials that have access to write to your bucket  
- The dogestry docker must access docker deamon with already built containers that you're planning to store. For that we specify the address via socket to docker daemon: `-v /var/run/docker.sock:/var/run/docker.sock`  
- `dogestry` we specify the docker to run  
- `dogestry push` we call executable from the inside of the `dogestry` container with parameter `push`  
- `s3:///aws-s3-bucket-name/folder` address to your s3 bucket via s3 protocol and don't forget triple :///  
- `name-of-your-pushed-container` name of the container image you wanna push  

Let's hope it works for you too!
