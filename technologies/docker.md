Docker containerizes code for consistent and reproducible execution across different machines.

> Container = package of code + dependencies to run code

# How to use docker

1. Create `Dockerfile` which is a script that contains a set of instructions for building a Docker image

DockerFile :

```
FROM node:14

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 3000

CMD [ "node", "app.mjs" ]
```

2. Run `docker build .` to build a docker image

3. Run `docker run -p 3000:3000 58ee4942eb1a` , runs the docker image (58ee4942eb1a) on port 3000
