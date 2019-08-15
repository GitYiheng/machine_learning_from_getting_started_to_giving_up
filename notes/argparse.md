# Argparse

Argparse helps you make command-line interface in Python.

https://docs.python.org/3/library/argparse.html

## Install argparse on Ubuntu 18.04

```
pip install argparse
```

## A Minimum Example

Create a Python script `add.py`:

```python
import argparse

# create a parser
parser = argparse.ArgumentParser(description='Add two values.')

# add arguments
parser.add_argument('--numbera', type=int, metavar='', required=True, help='First value')
parser.add_argument('--numberb', type=int, metavar='', required=True, help='Second value')

# parse arguments
args = parser.parse_args()

def add(a, b):
    return (a+b)

if __name__ == '__main__':
    sum = add(args.numbera, args.numberb)
    print(sum)
```

Test it in command-line:

```
python add.py --numbera=1 --numberb=2
```
Test it in command-line:

```
python add.py --numbera=1 --numberb=2
```
## Mutually Exclusive Group

Edit the Python script `add.py`:

```python
import argparse

# create a parser
parser = argparse.ArgumentParser(description='Add two values.')

# add arguments
parser.add_argument('--numbera', type=int, metavar='', required=True, help='First value')
parser.add_argument('--numberb', type=int, metavar='', required=True, help='Second value')

# mutually exclusive group
group = parser.add_mutually_exclusive_group()
group.add_argument('--quiet', action='store_true', help='Quiet version')
group.add_argument('--verbose', action='store_true', help='Verbose version')

# parse arguments
args = parser.parse_args()

def add(a, b):
    return (a+b)

if __name__ == '__main__':
    sum = add(args.numbera, args.numberb)
    # only one can be true
    if args.quiet:
        print(sum)
    elif args.verbose:
        print("The sum of %s and %s is %s" % (args.numbera, args.numberb, sum))
    else:
        print("The sum is %s" % sum)
```

Test it in command-line:

```
python add.py --numbera=1 --numberb=2
python add.py --numbera=1 --numberb=2 --quiet
python add.py --numbera=1 --numberb=2 --verbose
```
