# thelounge-k8s
A trivial kubernetes deployment for the official docker images of [thelounge.chat](https://thelounge.chat/).

To deploy:

    $ kubectl apply -f <this directory>

To create and manage users you need to log into the pod and directly execute thelounge commands:

    $ kubectl exec -ti thelounge-xxxxxxx-yyyyyyy /bin/bash
    
    $ thelounge list
    2020-07-23 08:23:12 [INFO] Users:
    2020-07-23 08:23:12 [INFO] 1. mbooth

You will additionally need to create an Ingress/Route for the service in order to access it externally. I haven't included this, as it's specific to your cluster.

## Implementation notes
Note that we set the data directory to be one level lower than the mountpoint of the data volume. This is because the application chowns its data directory at startup. This will fail on the volume mount point, preventing the service from starting.

I don't really like the config being stored in the mounted volume, but I couldn't see an option to move it.
