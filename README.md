# Some `uv` Dockerfile examples

## Simplest case
- `uv`is installed and remains in the container
- we don't care if dev dependencies remain
- we're happy to use `uv run` to execute our command

[Dockerfile](https://github.com/shaunhegarty/uv-docker-examples/blob/main/Dockerfile.single.uvrun)

To run:
```bash
docker build -f Dockerfile.single.uvrun -t uv-single-uvrun .
docker run --rm uv-single-uvrun
```

## Run with python
- We don't want to include dev-dependencies
- `uv run` effectively runs `uv sync` before each, meaning we always need to include `--no-dev` in any case where `uv run` is used or we'll end up installing the packages in each container or syncing the environment each time `uv run` is called. 

[Dockerfile](https://github.com/shaunhegarty/uv-docker-examples/blob/main/Dockerfile.single.python)

To run:
```bash
docker build -f Dockerfile.single.python -t uv-single-python .
docker run --rm uv-single-python
```

## Multi-stage build
- We want to use a multi-stage build to keep the image size down

[Dockerfile](https://github.com/shaunhegarty/uv-docker-examples/blob/main/Dockerfile.multi.python)
    
To run:
```bash
docker build . -f Dockerfile.multi.python -t uv-multi-python
docker run --rm uv-multi-python
```

## Multi-stage build using alpine
- Use alpine to keep the image size down even more

[Dockerfile](https://github.com/shaunhegarty/uv-docker-examples/blob/main/Dockerfile.multi.python.alpine)

To run:
```bash
docker build . -f Dockerfile.multi.python.alpine -t uv-multi-python-alpine
docker run --rm uv-multi-python-alpine
```

## Image size comparison:
```bash
uv-single-uvrun                454MB
uv-single-python               267MB
uv-multi-python                240MB
uv-multi-python-alpine         168MB
```	

