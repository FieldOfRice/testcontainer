# Testcontainers Redis Example

This repository shows a minimal working example of using
[Testcontainers for Python](https://testcontainers-python.readthedocs.io/en/latest/)  
to spin up a temporary **Redis** instance for integration tests.

By using Testcontainers, you don’t have to install Redis locally —  
it runs in a lightweight Docker container and is automatically cleaned up after tests.

## Features
- Runs Redis in a container automatically for tests
- No manual setup required
- Works with pytest
- Cleans up after runs

## Requirements
- Python 3.10+
- Docker installed and running

## Installation

```
git clone https://github.com/<name>/testcontainer.git
cd testcontainer
uv sync
uv run python - <<EOF
from testcontainers.redis import RedisContainer
import redis

def test_redis_container():
  with RedisContainer() as redis_container:
    redis_client = redis_container.get_client(decode_responses=True)
    redis_client.set("Greeting", "Hello world")
    value = redis_client.get("Greeting")
    print(f"Value of Greeting is {value}")
    assert value == "Hello world"

if __name__ == "__main__":
  print(">>> start redis test synchronously")
  test_redis_container()

print(f">>> done");
EOF
```
