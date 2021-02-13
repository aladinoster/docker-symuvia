# Buid SymuVia 

Containerized version of Symuvia. 

## Obtain 

Get the Docker file to create the container via:

```
  git clone https://github.com/licit-lab/docker-symuvia.git
```


## Build 

Go inside `docker-symuvia/symupy`. This container has inside a compiled version of the traffic simulator [symuvia](https://github.com/licit-lab/symudev) + a package to interact [symupy](https://symupy.readthedocs.io/en/stable/)

```
 docker build --rm -f "Dockerfile" -t local:symuvia "." 
```

**Note**: Source files are not included for licenses purposes. 


## Run 

Run the container in a terminal consol via

```
  docker run --rm -it -p 8888:8888 local:symuvia
```

Launch Jupyter lab via 

```
jupyter lab --notebook-dir=/home/ --ip='0.0.0.0' --port=8888 --no-browser --allow-root
```
