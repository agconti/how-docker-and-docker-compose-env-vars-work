# How to env vars get passed to a dockerfile? 
Follow this journey. 

View the output of the script to understand how env vars are exposed durning the build and runtime stages with docker and docker-compose. Short answer is that:

- Dockerfile's do not have access to the env vars in your environment
- ENV commands in a dockerfile just set an env var for each command _in the dockerfile_. They are *not* env vars as you would think of them and they do not show up at runtime
- ARG commands allow us to provide values for the ENV statement in our dockerfile. We can use ARGs to pull form the *real* env vars in our environment

# Why?
https://github.com/docker/compose/issues/5600#issuecomment-450920704

# View demo
```bash
./run.sh
```