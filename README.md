
## docker hub push pull run Command
docker build -t ranjeethmd/open-image:core-worker-image .

docker image push ranjeethmd/open-image:core-worker-image

docker run -d  --name core-worker-container ranjeethmd/open-image:core-worker-image