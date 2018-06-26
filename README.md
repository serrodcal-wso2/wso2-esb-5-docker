# Docker image for WSO2 ESB 5

This is a own image for WSO2 ESB 5.0.0. Its purpose is to be able to be deployed in any environment, even in production.

## Getting started

### Prerequisites

Please, clone this repository in your local by `~$ git clone https://gitlab.com/serrodcal/wso2-esb-5-docker.git`. Or try it using SSH by `~$ git clone git@gitlab.com:serrodcal/wso2-esb-5-docker.git` if your prefer.

Now, please download WSO2 ESB 5.0.0 product from [official website](https://wso2.com/integration/previous-releases) and put it into local project which just download previously.

### Building

Once into `wso2-esb-5-docker/` directory, let's go to build this image by `~$ docker build -t <own_name> .`, and set your own docker image name. Or try to pulling from Docker Hub (recommended) by `~$ docker pull serrodcal/wso2esb5:0.1.0`.

### Running

Let's run it by `~$ docker run -d --name esb1 serrodcal/wso2esb5:0.1.0 `. If you built the image using your own docker image name, please change _wso2esb5:0.1.0_ by your name.

This image has following params as environment variable (with default values): 

```
ARG JAVA_OPTS="-Xms2048m -Xmx2048m"
ARG OSGI_CONSOLE_PORT=19444

ENV JAVA_OPTS ${JAVA_OPTS}
ENV OSGI_CONSOLE_PORT ${OSGI_CONSOLE_PORT}
```

Also, expose following ports: `8280 8243 9763 9443 ${OSGI_CONSOLE_PORT}`. Execute `~$ docker run -d --name esb1 -p 8280:8280 -p 8243:8243 -p 9763:9763 -p 9443:9443 -p 19444:19444 serrodcal/wso2esb5:0.1.0` to access by those ports.

### Testing

For testing, there is a shell script named `run_tests.sh` which checks the server is up and running fine. And also there is another Dockerfile for testing named `Dockerfile-Test`.

How to test it? In this case, we use following steps:

```bash
docker build -t serrodcal/wso2esb5-test:0.1.0 -f Dockerfile-Test .
docker run -d --name esb1-test serrodcal/wso2esb5-test:0.1.0
docker logs esb1-test -f
```

Wait until `Test passed.` message appears. Other messages mean the test failed.


### Provisioning

There are several ways to provisioning this, for instance, create your own Docker image using FROM in your Dockerfile and use ADD/COPY to `carbonapps` subdirectory. Other way is to use Docker volumes. We recommend use both, create your own image with your own componentes and use Docker volumes to configure by environments.

## Built with

* [Docker](https://www.docker.com/) - Platform containerization
* [WSO2 ESB 5.0.0](https://wso2.com/) - Enterprise integrator middleware

## Versioning

We use _X.Y.z_ for versioning. For the versions available, see the tags on this repository.

## Authors

* Sergio Rodríguez Calvo

## License

This project is under [GNU General Public License v3.0](https://github.com/serrodcal/wso2-esb-5-docker/blob/master/LICENSE).
