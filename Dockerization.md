# How to create the container for the competition.

## Requirements
All the dockers for the competition are encouranged to use the following:
1. OS: Linux. Alpine specifically as the base for the official python:3.10 docker image.
2. Docker version: 23.0.0

The infrastructure was tested with the Linux Alpine as part of the base layer official python:3.10, and dockers built on version 23.0.0 of the docker engine.
Using other Linux based OS and other docker engine version might be possible but has not been tested, use them on your own risk.

## Docker Template

A template github for the noop agent is provided as a starting point:
- [https://github.com/ataitler/RDDL-demo-agent](https://github.com/ataitler/RDDL-demo-agent). The github also provides details on how to run and create your docker. The packaged image of the repository above is available through docker-hub at:
- [docker://ataitler/rddl-demo-agent](docker://ataitler/rddl-demo-agent)

For those of you who are new to docker, we recommand a quick crash course:
- [Dockers for begginers](https://docker-curriculum.com/)


**Important**: It is _**mandatory**_ to clone/fork this template, and populate it with your own method as your docker must contain as entrypoint the main.py file from that repo. The interaction loop, timers, and pyRDDLGym interaction for the competition are included in that file and not externally. This is to allow for simple "local" like interaction, and transperancy of the competition procedure. As described in the template repo, your method will interact with a competition version of pyRDDLGym installed by us on our server and mapped to your container. Using the template will ensure correct interaction with the pyRDDLGym server.

### Example run

The dockers will rebuilt and executed on our HPC using the Singularity infrastructure. Thus, complying with the instructuins is crucial for the transition to work smoothly (full paths, etc.).

In order to test your method on your own side and making sure everyting work, we provide an example of how to run the docker once built.

In this example we cloned pyRDDLGym to the local user _test_ home folder under Downloads, i.e., `/home/test/Downloads/pyRDDLGym`. We will bind that folder as an external volume for the docker, at the local path `/usr/share/pyRDDLGym`. This path will also be added to the environment variable PYTHONPATH of the docker so your imports will work.

We wish to run the noop rddl-demo-agent image for the HVAC domain, instance 0, for 50 trials. Our method name is "_my_method_". The excution line will be:

```bash
docker run -v /home/test/Downloads/pyRDDLGy:/usr/share/pyRDDLGym 
           -e PYTHONPATH="$PYTHONPATH:/usr/share/pyRDDLGym" rddl-demo-agent HVAC 0 my_method 50
```
