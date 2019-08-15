# Customized OpenAI Gym Environment

You might want to create your own Gym environment.

## Create This File Structure

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

## Copy and Paste Following Code to Corresponding Scripts

`gym-foo/setup.py`
```python
from setuptools import setup

setup(name='gym_foo',
      version='0.0.1',
      install_requires=['gym']
)
```

`gym-foo/gym_foo/__init__.py`
```python
from gym.envs.registration import register

register(
    id='foo-v0',
    entry_point='gym_foo.envs:FooEnv',
)
```

`gym-foo/gym_foo/envs/__init__.py`
```python
from gym_foo.envs.foo_env import FooEnv
```

`gym-foo/gym_foo/envs/foo_env.py`
```python
import gym

class FooEnv(gym.Env):
    def __init__(self):
        pass
    
    def step(self, action):
        pass
    
    def reset(self):
        pass
    
    def render(self, mode='human', close=False):
        pass
```

## Go to `gym-foo/` Directory and Install the Customized Gym Environment

```
pip install -e .
```

## Now the Customized Gym Environment is Ready to Use

```python
import gym
import gym_foo
env = gym.make('foo-v0')
```
