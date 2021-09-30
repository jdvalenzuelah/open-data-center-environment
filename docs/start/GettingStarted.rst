***************
Getting Started
***************

#. Install Docker and run the Docker daemon

#. Download Dockerfile

#. Change dir to the Dockerfile and build it
   ::
        
        $ docker build --tag opendce:latest .
#. Run the container and publish the port (Add `-d` to run in the background)
   ::
    
        $ docker run --volume  $(pwd)/notebooks:/home/openmodelicausers/notebooks \
                     --publish 8888:8888 opendce:latest


   .. note::

        If error: ``docker: Error response from daemon: cgroups: cgroup mountpoint does not exist: unknown``:
        Temp fix: https://github.com/docker/for-linux/issues/219#issuecomment-375160449
        ::

            $ sudo mkdir /sys/fs/cgroup/systemd
            $ sudo mount -t cgroup -o none,name=systemd cgroup /sys/fs/cgroup/systemd
        
        If running on apple silicon devices omc and omlib-modelica installation will fail since openmodelica provides packages just for x86, amd64, and armv7
        to avoid such error you can add ``--platform linux/amd64`` to docker build command https://docs.docker.com/desktop/mac/apple-silicon/

#. Copy notebooks
   ::

        $ docker cp ./notebooks/Modelica\ by\ Example.ipynb <containerID>:/home/openmodelicausers/notebooks

#. Stop the container and remove
   ::

        $ docker container stop opendce:latest
        $ docker container rm   opendce:latest
        $ docker volume    rm   volume_name

