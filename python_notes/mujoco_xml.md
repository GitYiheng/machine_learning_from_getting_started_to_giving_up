# MuJoCo .xml Model

You can build models for MuJoCo in .xml format.

# qpos

The first 3 elements in qpos describe the position

    qpos[0]~qpos[2]: body position

The next 4 elements in qpos describe the orientation

    qpos[3]~qpos[6]: body orientation (in quaternion)

The following elements correspond to the rest joints define in sequence

    qpos[n]: joint n

# Quaternion

Quaternion describes 3d orientation using 4 numbers.

a + b**i** + c**j** +d**k**

a describes the distance, while b, c, and d describe the orientation.

