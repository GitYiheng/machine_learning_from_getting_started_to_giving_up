# Create Directories

You can create directories in Python using the `os` module.

# File Path

```python
import os

print("File path:")
print(os.path.realpath(__file__))
```

# File Directory Path

```python
import os

print("File directory path:")
print(os.path.dirname(os.path.realpath(__file__)))
```

# New Directory Path

```python
import os

print("New directory path:")
print(os.path.join(os.path.dirname(os.path.realpath(__file__)), "new_dir"))
```

# Create Directory

```python
import os

new_dir = os.path.join(os.path.dirname(os.path.realpath(__file__)), "new_dir")
os.makedirs(new_dir, exist_ok=True) # By setting exist_ok as True error caused due already existing directory can be suppressed 
```
