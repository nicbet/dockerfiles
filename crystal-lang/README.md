# Crystal Language Dockerfile

# Building
`docker build -t crystal-lang:latest -f Dockerfile.ubuntu.latest .`

# Usage

### Cross-Compilation
```
docker run --rm -it -v `pwd`:/opt/crystal crystal-lang:latest crystal build src/server.cr --no-debug -o ./server
```

### Execution
```
docker run --rm -it -v `pwd`:/opt/crystal crystal-lang:latest ./server
```
