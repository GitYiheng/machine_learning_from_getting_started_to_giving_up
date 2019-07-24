# Multithreading and Multiprocessing

Both multithreading and multiprocessing run different programs at the same time, which use waiting time of some programs to do useful things for other programs.

The multithreading module `threading` uses threads, while the multiprocessing module `multiprocessing` uses processes.

Different threads run in the same CPU and use the same memory, while different processes run in different CPUs and have separate memories.

Sharing objects between processes is a bit harder but spawning processes is a bit slower.

# Example

`vanilla.py`
```python
import time

def calc_square(numbers):
    print("calculate square numbers")
    for n in numbers:
        time.sleep(0.2)
        print("square:", n*n)

def calc_cube(numbers):
    print("calculate cube of numbers")
    for n in numbers:
        time.sleep(0.2)
        print("cube:", n*n*n)

if __name__ == "__main__":
    arr = [2, 3, 8, 9]
    t = time.time()
    calc_square(arr)
    calc_cube(arr)
    print("It takes ", time.time()-t)
```

`multithreading.py`
```python
import time
import threading

def calc_square(numbers):
    print("calculate square numbers")
    for n in numbers:
        time.sleep(0.2)
        print("square:", n*n)

def calc_cube(numbers):
    print("calculate cube of numbers")
    for n in numbers:
        time.sleep(0.2)
        print("cube:", n*n*n)

if __name__ == "__main__":
    arr = [2, 3, 8, 9]
    t = time.time()
    t1 = threading.Thread(target=calc_square, args=(arr,))
    t2 = threading.Thread(target=calc_cube, args=(arr,))
    t1.start()
    t2.start()
    t1.join()
    t2.join()
    print("It takes ", time.time()-t)
```

`multiprocessing.py`
```python
import time
import multiprocessing

square_result = []

def calc_square(numbers):
    global square_result
    print("calculate square numbers")
    for n in numbers:
        time.sleep(0.2)
        print("square:", n*n)
        square_result.append(n*n)
    print("Inside the process, result: ", square_result)

def calc_cube(numbers):
    print("calculate cube of numbers")
    for n in numbers:
        time.sleep(0.2)
        print("cube:", n*n*n)

if __name__ == "__main__":
    arr = [2, 3, 8, 9]
    t = time.time()
    p1 = multiprocessing.Process(target=calc_square, args=(arr,))
    p2 = multiprocessing.Process(target=calc_cube, args=(arr,))
    p1.start()
    p2.start()
    p1.join()
    p2.join()
    print("Outside the process, result: ", square_result)
    print("It takes ", time.time()-t)
```
