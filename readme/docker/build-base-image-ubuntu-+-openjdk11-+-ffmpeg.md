# Build base image : ubuntu + openjdk11 + ffmpeg

## DockerFile

```docker
FROM ubuntu:22.04
RUN apt update
RUN apt install openjdk-11-jdk -y
RUN apt install ffmpeg -y
```



## Image Build

<pre class="language-bash"><code class="lang-bash"><strong>$ docker build --platform linux/amd64 \
</strong> -t base-image/adoptopenjdk/openjdk11-ffmpeg:20230711 \
 -f ./DockerFile .
$ docker tag base-image/adoptopenjdk/openjdk11-ffmpeg:20230711 \
 &#x3C;ECR_PATH>/base-image/adoptopenjdk/openjdk11-ffmpeg:20230711
</code></pre>



## ECR Push

<pre class="language-bash"><code class="lang-bash"><strong>$ aws sso login --profile &#x3C;PROFILE_NAME>
</strong>$ aws ecr get-login-password --profile &#x3C;PROIFLE_NAME> \
 --region &#x3C;REGION_NAME> | docker login --username AWS --password-stdin &#x3C;ECR_PATH>
$ docker push &#x3C;ECR_PATH>/base-image/adoptopenjdk/openjdk11-ffmpeg:20230711
</code></pre>
