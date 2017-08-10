# Gateway

This is the gateway service for datawire cloud applications. The
purpose of this service is to provide authentication, routing, and
metrics for services within the cluster.
   
## Directory layout:

This application is layed out as a monorepo for convenience, however
each service directory is independently releasable, and all the
tooling provided will work seamlessly with a one repo per service
layout.

```
 <root>
   |
   |               API Gateway
   |
   +--- service.yaml        (service metadata for forge)
   |
   +--- Dockerfile          (dockerfile that builds the API Gateway)
   |
   +--- k8s/deployment.yaml (deployment templates for the API gateway)
   |
   |
   +--- auth                  Authentication Service
   |     |
   |     +--- service.yaml        (service metadata for forge)
   |     |
   |     +--- Dockerfile          (dockerfile that builds the authentication service)
   |     |
   |     +--- k8s/deployment.yaml (deployment templates for the auth service)
   |     |
   |     +--- app.py              (auth service implementation)
   |
   |
   +--- prometheus             Search Service
   |     |
   |     +--- service.yaml        (service metadata for prometheus)
   |     |
   |     +--- Dockerfile          (dockerfile that builds prometheus container)
   |     |
   |     +--- k8s/deployment.yaml (deployment templates for prometheus)
   |     |
   |     +--- index.html          (skeletal console template for prometheus)
   |
   |
   +--- ...
   |
   .
   .
```

## Developing

### Prerequisites

You will need the following installed locally:

* Python 2.7 or later
* Docker
* kubectl, configured to talk to the cluster where you want to deploy the application
* An account with a Docker Registry (e.g., Google Container Registry or Docker Hub)
* [Forge](http://forge.sh)

### Deploying a change

1. Edit any files you would like to change.

2. Run: `forge deploy`

This will redeploy any pieces necessary. Note that `forge deploy` will
figure out what services to operate on based on the current working
directory. If you want to deploy a change to just one service
(e.g. just the auth service), cd into `auth` and run `forge deploy`
from there.
