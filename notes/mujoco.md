# MuJoCo

Use MuJoCo as your physics simulator if you want your paper get accepted.

http://www.mujoco.org/

I use mujoco-py for Python3 on Ubuntu 18.04.

https://github.com/openai/mujoco-py

## Get a License

Your aim is to get the file `mykey.txt`:

1. Apply for a license on https://www.roboti.us/license.html and you will get an account number by email.

2. Download `getid_linux` on https://www.roboti.us/license.html and use your account number to generate your computer id.

```
chmod +x getid_linux
./getid_linux
```

3. Fill your account number and computer id on https://www.roboti.us/license.html and you will get `mjkey.txt` by email.

## Install MuJoCo

1. Download `mujoco200 linux` from https://www.roboti.us/index.html.

2. Unzip it to `~/.mujoco/mujoco200` and put your license to `~/.mujoco/mjkey.txt`.

3. `sudo nano ~/.bashrc` and add following lines:

```
export LD_LIBRARY_PATH=/home/<user_name>/.mujoco/mujoco200/bin
export PATH="$LD_LIBRARY_PATH:$PATH"
export LD_PRELOAD=/usr/lib/x86_64-linux-gnu/libGLEW.so
```

4. `source ~/.bashrc`

5. Test MuJoCo

```
cd ~/.mujoco/mujoco200/bin
./simulate
```

## Install mujoco-py

1. Install required packages

```
sudo apt-get update
sudo apt-get install -y patchelf python3 python3-dev build-essential libssl-dev libffi-dev libxml2-dev libxslt1-dev zlib1g-dev libglew1.5 libglew-dev libgl1-mesa-dev libgl1-mesa-glx libosmesa6-dev python3-pip python3-numpy python3-scipy
```

2. Install mujoco-py

```
git clone https://github.com/openai/mujoco-py.git
cd mujoco-py
pip install -e .
```

3. Test mujoco-py

```python
import mujoco_py
import os
mj_path, _ = mujoco_py.utils.discover_mujoco()
xml_path = os.path.join(mj_path, 'model', 'humanoid.xml')
model = mujoco_py.load_model_from_path(xml_path)
sim = mujoco_py.MjSim(model)
print(sim.data.qpos)
sim.step()
print(sim.data.qpos)
```
