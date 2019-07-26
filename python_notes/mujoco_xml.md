# MuJoCo .xml Model

You can build models for MuJoCo in .xml format.

# qpos

Every 'body' start with 7 elements.

The first 3 elements in qpos describe the position

    qpos[0]~qpos[2]: x, y, and z coordinate of that 'body'

The next 4 elements in qpos describe the orientation

    qpos[3]~qpos[6]: orientation in quaternion of that 'body'

The following elements correspond to the rest joints define in that 'body'

    qpos[7]: joint 1 of that 'body'
    qpos[8]: joint 2 of that 'body'
    ...

# Quaternion

Quaternion describes 3d orientation using 4 numbers.

a + b**i** + c**j** +d**k**

a describes the distance, while b, c, and d describe the orientation.

