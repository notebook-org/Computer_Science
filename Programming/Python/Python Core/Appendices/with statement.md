# with statement
* with statement in Python is used in exception handling to make the code cleaner and much more readable.

```python
# without using with statement
file = open('file_path', 'w')
try:
    file.write('hello world')
finally:
    file.close()

# using with statement
with open('file_path', 'w') as file:
    file.write('hello world !')
```

* There is no need to call file.close() when using with statement.
    * The with statement itself ensures proper acquisition and release of resources.

## Reference
* [with statement](https://www.geeksforgeeks.org/with-statement-in-python/)
