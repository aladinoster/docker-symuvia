# Buid SymuVia 

Containerized version of Symuvia. 

## Obtain 

Get the executable container via:

```
  git clone https://github.com/aladinoster/docker-symuvia.git
```


## Build 

Go inside `docker-symuvia/symupy`

```
 docker build --rm -f "Dockerfile" -t local:symuvia "." 
```

**Note**: Source files are not included for licenses purposes. 


## Run 

```
  docker run --rm -it -p 8888:8888 local:symuvia
```

Launch Jupyter lab via 

```
jupyter lab --notebook-dir=/home/ --ip='0.0.0.0' --port=8888 --no-browser --allow-root
```
