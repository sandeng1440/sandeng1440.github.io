+++
date = '2025-11-03T22:19:06+03:00'
draft = false
title = 'Map, Filter & Reduce'
+++
# Map, Filter & Reduce
**Map, filter and reduce** are the 3 functions that power **functional programming**. In this article, we'll learn how they work and implement them in Golang. 

---

## Map
The `map(f, iterable)` function takes a function, `f` and applies it to every element of the `iterable` (array, list, tuple, set).
```go
func myMap(f func, iterable interface{})
```
