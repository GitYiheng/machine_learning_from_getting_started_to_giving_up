# OpenAI Gym and MuJoCo Tutorials

## How to make a custom gym environment?

## 1. Create a file structure as follows

```
gym-foo/
    README.md
    setup.py
    gym_foo/
        __init__.py
        envs/
            __init__.py
            foo_env.py
```

You can change `foo` to your environment name.

## 2. Copy and paste following code snippets to corresponding scripts

### gym-foo/setup.py
```python
from setuptools import setup

setup(name='gym_foo',
      version='0.0.1',
      install_requires=['gym']
)
```

### gym-foo/gym_foo/__init__.py
```python
from gym.envs.registration import register

register(
    id='foo-v0',
    entry_point='gym_foo.envs:FooEnv',
)
```

### gym-foo/gym_foo/envs/__init__.py
```python
from gym_foo.envs.foo_env import FooEnv
```

### gym-foo/gym_foo/envs/foo_env.py
```python
import gym
from gym import error, spaces, utils
from gym.utils import seeding

class FooEnv(gym.Env):
    metadata = {'render.modes': ['human']}
    
    def __init__(self):
        pass
    
    def step(self, action):
        pass
    
    def reset(self):
        pass
    
    def render(self, mode='human', close=False):
        pass
```

## 3. Go to `gym-foo/` directory and install the custom gym environment by typing

```
pip install -e .
```

## 4. Now the custom gym environment is ready to use in Python

```python
import gym
import gym_foo
env = gym.make('foo-v0')
```
