# MuJoCo .xml Model

You can build models for MuJoCo in .xml format.

# qpos

The first 3 elements in qpos describe the position of 'worldbody'

    qpos[0]~qpos[2]: world position

The following 7 elements in qpos describe the position and orientation of that 'body'

    qpos[3]~qpos[5]: body position

    qpos[6]~qpos[9]: body orientation (in quaternion)

In a similar way, the next 7 elements in qpos describe the position and orientation of the next 'body'

    qpos[10]~qpos[12]: body position

    qpos[13]~qpos[16]: body orientation (in quaternion)

