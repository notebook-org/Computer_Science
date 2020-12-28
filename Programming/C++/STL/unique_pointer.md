## Unique Pointer
* It is a scoped pointer when that pointer goes out of scope, it will be distroyed and it will call delete.
* You cannot have a copy of a unique pointer
```C++
std::unique_ptr<ClassName> object_name = std::make_unique<ClassName>();
```