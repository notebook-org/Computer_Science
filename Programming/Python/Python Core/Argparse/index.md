# Argparse

## References
* [Argparse Tutorial Link](https://docs.python.org/3/howto/argparse.html)

# Argparse Tutorial
* The recommended command-line parsing module in the Python standard library

**positional argument:** It's named so because the program should know what to do with the value, solely based on where it appears on the command line.

**optional argument:** Example -l in ls command

```python
import argparse
parser = argparse.ArgumentParser()
args = parser.parse_args()
```

## Introducing Positional arguments

```python
parser.add_argument("echo")
or
parser.add_argument("echo", help="echo the string you use here")
parser.add_argument("square", help="display a square of a given number", type=int)
```
## Introducing Optional arguments

```python
parser.add_argument("--verbosity", help="increase output verbosity")
```

```sh
$ python3 prog.py --verbosity 1
> verbosity turned on
```

* When using the --verbosity option, one must also specify some value, any value.

```python
parser.add_argument("--verbose", help="increase output verbosity",
                    action="store_true")
```

```sh
$ python3 prog.py --verbosity
> verbosity turned on
```

* The option is now more of a flag than something that requires a value.
* Note that we now specify a new keyword, action, and give it the value "store_true". This means that, if the option is specified, assign the value True to args.verbose. Not specifying it implies False.

#### Short options

```python
parser.add_argument("-v", "--verbose", help="increase output verbosity",
                    action="store_true")
```

#### Multiple verbosity values

```python
parser.add_argument("-v", "--verbosity", type=int,
                    help="increase output verbosity")
```

#### Choices

```python
parser.add_argument("-v", "--verbosity", type=int, choices=[0, 1, 2],
                    help="increase output verbosity")
```

#### Count

```python
parser.add_argument("-v", "--verbosity", action="count", default=0,
                    help="increase output verbosity")
```

## Reference
* [Docs Link](https://docs.python.org/3/howto/argparse.html)
