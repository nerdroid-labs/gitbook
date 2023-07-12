# Build base image : openjdk11 + ffmpeg

## DockerFile

```docker
FROM adoptopenjdk/openjdk11:jdk-11.0.18_10-alpine
RUN apk update && apk add ffmpeg
```



## Image Build

<pre class="language-bash"><code class="lang-bash"><strong>docker build --platform linux/amd64 \
</strong> -t argo-base/adoptopenjdk/openjdk11-ffmpeg:20230711 \
 -f ./DockerFile .
docker tag argo-base/adoptopenjdk/openjdk11-ffmpeg:20230711 \
 &#x3C;ECR_PATH>/argo-base/adoptopenjdk/openjdk11-ffmpeg:20230711
</code></pre>



## ECR Push

```bash
aws ecr get-login-password --profile <PROIFLE_NAME> \
 --region <REGION_NAME> | docker login --username AWS --password-stdin <ECR_PATH>
docker push <ECR_PATH>/argo-base/adoptopenjdk/openjdk11-ffmpeg:20230711
```
