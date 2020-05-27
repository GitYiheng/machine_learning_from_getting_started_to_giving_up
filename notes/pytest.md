# pytest

The `pytest` framework makes it easy to write small tests, yet scales to support complex functional testing for applications and libraries.

## Installation

```
pip install -U pytest
```

## Check Version

```
pytest --version
```

## Example

```python
# content of test_sample.py
def func(x):
    return x + 1

def test_answer():
    assert func(3) == 5
```
