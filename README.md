# Buid SymuVia 

Containerized version of Symuvia. 

## Obtain 

Get the executable container via:

```
  git clone https://github.com/aladinoster/docker-symuvia.git
```


## Build 

Go inside `docker-symuvia/build-symuvia`

```
 docker build --rm -f "Dockerfile" -t local:symuvia "." 
```

**Note**: Source files are not included for licenses purposes. 


## Run 

```
  docker run --rm -it local:symuvia
```
