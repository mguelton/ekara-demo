# Ekara demo

This repository shows how Ekara can:

* Create an infrastructure (on AWS here),
* Install an container orchestrator (Docker Swarm here),
* Deploy software stacks:
  * Applicative stacks (a trivial "Hello World" application),
  * On-the-shelf stacks (a Swarm visualizer).

## Running the demo

To run the demo, create a `vars.yaml` file with the following contents (adapted to your chosen values):

```
ek:
  aws:
    region: eu-west-1
    accessKey: 
      id: __YOUR_AWS_KEY__
      secret: __YOUR_AWS_SECRET__

app:
  visualizer:
    port: 8080
  app:
    port: 80
```

The file above will be used as external variables to template the demo. Then download the latest [Ekara CLI](https://github.com/ekara-platform/cli/releases), put it in your path and run:

```
$ ekara deploy https://github.com/ekara-platform/demo -p vars.yaml -l
```

This will:

1. Create the security groups, machines and volumes on AWS.
2. Install the required packages, Docker CE and setup a Swarm cluster on the nodes.
3. Deploy:
  * The Ekara core stack (Hashicorp Consul + Ekara API)
  * The Swarm visualizer
  * The "Hello World" application (Redis + Python app)

A lot of actions are executed so this may take a while (usually around 10 minutes). You can run the `light` branch instead which deploy the same stacks to a unique machine and is faster to deploy:

```
$ ekara deploy https://github.com/ekara-platform/demo@light -p vars.yaml -l
```
