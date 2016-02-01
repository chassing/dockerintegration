# Docker Integration

[![Build Status](https://travis-ci.org/ShaneDrury/dockerintegration.svg?branch=master)](https://travis-ci.org/ShaneDrury/dockerintegration)

Control Docker from within Python scripts.
Set-up and tear-down for integration tests.

## Installation

```python
pip install dockerintegration
```

## Example Usage

# py.test

```python
# conftest.py
from dockerintegration.testing import docker_fixture
```

```python
# test_redis.py
from redis import StrictRedis

def test_push_to_redis(docker_fixture):
    container = docker_fixture.services['redis'][0]
    host_address = container.addresses[6379][0]
    redis = StrictRedis(host=host_address.ip, port=host_address.port)
    redis.rpush('key', ['value'])
    ...

# or

def test_push_to_redis_better(docker_fixture):
    host_address = docker_fixture.get_first_container_address('redis', 6379)
    redis = StrictRedis(host=host_address.ip, port=host_address.port)
    redis.rpush('key', ['value'])
    ...
```


## TODO

- Test set-up for unittest
- wait until up for services - optional, may depend on service
