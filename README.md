# How do env vars get passed to a Dockerfile? 
Follow this journey. 

View the output of the script to understand how env vars are exposed during the build and runtime stages with docker and docker-compose. 

The short answer is that:

- Dockerfile's do not have access to the env vars in your environment
- ENV commands in a dockerfile just set an env var for each command _in the dockerfile_. They are *not* env vars as you would think of them and they do not show up at runtime
- ARG commands allow us to provide values for the ENV statement in our dockerfile. We can use ARGs to pull from the *real* env vars in our environment

# Why?
https://github.com/docker/compose/issues/5600#issuecomment-450920704

# View demo
```bash
./run.sh
```

# Demo output
```bash
#1 [internal] load build definition from Dockerfile
#1 sha256:29a546d4fe90cd434f52fa3bf3683f953e5474c7b92c8428a87c3b741f21ed4d
#1 transferring dockerfile: 409B done
#1 DONE 0.0s

#2 [internal] load .dockerignore
#2 sha256:423493d4de28cd8309e87823f167fbf4f07c7e94f35a347adde1b7a7219d898c
#2 transferring context: 2B done
#2 DONE 0.0s

#3 [internal] load metadata for docker.io/library/bash:latest
#3 sha256:9f18c0109e26dd11a5238345e974f9ea7b9679be4afd445b93308bf709f74057
#3 DONE 0.2s

#4 [1/4] FROM docker.io/library/bash@sha256:a2ec07de39cf5efd201ceb04403e1762ea296fb1c5d4b7e2175c11c8bf0b7f71
#4 sha256:6645f5e6d5c950042cb6e1488aa51da49a64c3488b6397374cb0fca572594065
#4 DONE 0.0s

#6 [internal] load build context
#6 sha256:ef574b4f6c21b0e1e0eb97739b6964a37260cdf7cd46124099886b9ce0f8e4b6
#6 transferring context: 3.05kB 0.0s done
#6 DONE 0.0s

#5 [2/4] WORKDIR /app
#5 sha256:ef64cada5592a1ab45b9101f56eb300f35c72f95e30ea604fec7bd28d187e541
#5 CACHED

#7 [3/4] COPY . .
#7 sha256:7c3953d604ae6d36655b873abcec0d897e80576aab5ceb1d07bd7f1fb905a020
#7 DONE 0.0s

#8 [4/4] RUN ./script.sh
#8 sha256:63162cfa241f7aad61ec93efedc37443747aed010f7ed502b01f08cf780ab221
#8 0.443 
ENV_SPECIFED_IN_DOCKERFILE_AS_CONSTANT: yes 
ENV_SPECIFED_IN_DOCKERFILE_AS_ENV_VAR:
ENV_FROM_DOCKER_COMPOSE:
ENV_SPECIFED_IN_SHELL:
ENV_SPECIFED_IN_SHELL_PASSED_VIA_ARG_IN_COMPOSE: yes
#8 DONE 0.5s

#9 exporting to image
#9 sha256:e8c613e07b0b7ff33893b694f7759a10d42e180f2b4dc349fb57dc6b71dcab00
#9 exporting layers 0.1s done
#9 writing image sha256:9e104494fe9535a0254b16629c7c4967a8cef8afebb90c19ce331ae37002f156
#9 writing image sha256:9e104494fe9535a0254b16629c7c4967a8cef8afebb90c19ce331ae37002f156 done
#9 naming to docker.io/library/test-docker-env_test done
#9 DONE 0.1s
```