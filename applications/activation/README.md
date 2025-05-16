# buggy-app

This repository contains the Dockerfile and the nginx configurations used to generate a container image based on the official [nginx:alpine image](https://hub.docker.com/_/nginx/), slighty modified to run as a Red Hat OpenShift application.

You can easily build this image locally after checking out, running:

    $ docker image build -t <image-name>:<release> .

And Push it to the local OCP image registry

    $ oc get route default-route -n openshift-image-registry --template='{{ .spec.host }}'

    $ docker login -u $(oc whoami) -p $(oc whoami -t) default-route-openshift-image-registry.apps-crc.testing

    $ podman tag localhost/<image-name>:<release> default-route-openshift-image-registry.apps-crc.testing/shared-images/<image-name>:latest

    podman push --tls-verify=false default-route-openshift-image-registry.apps-crc.testing/shared-images/<image-name>:latest


