+++
date = '2025-11-03T22:19:06+03:00'
draft = false
title = 'Map, Filter & Reduce'
tags = ['functional programming', 'golang', 'holy trinity']
+++
**Map, filter and reduce** are the holy trinity of **functional programming**. These functions are available in all languages that encourage functional programming at the language level i.e Haskell as well as the multi-purpose languages such as Python and Javascript.
In this article, we'll learn how they work and implement them in Golang. 
Golang is not a functional programming language, but it gives us the tools to perform functional programming with the **generics**.

---

## Map
The map function is the first in the holy trinity of functional programming. The function `Map(iterable, f)` takes a function `f`, known as a **transform function**, and applies it to every element of the `iterable` (array, list, tuple, set).
In our case, we'll apply it to a slice of type T (generic type).
```go
// Simple map function that transforms a slice
func Map[T any](slice []T, transform func(T) T) []T {
	result := make([]T, len(slice))
	for _, elem := range slice { // index is ignored
		result = append(result, transform(elem)) // transform every element and append it to result
	}
	return result
}
```
## Filter
The filter function is the second in the holy trinity of functional programming. The function `Filter(iterable, f)` takes an iterable and returns all the elements that make the function `f` return `true`.
```go
func Filter[T any](slice []T, f func(T) bool) []T {
	var result []T
	for _, elem := range slice { // ignore index
		if f(elem) { // if f returns true, then
			result = append(result, elem) // append the elem to the result
		}
	}
	return result
}
```
## Reduce
The reduce function is the third function in the holy trinity of functional programming. This function `Reduce(iterable, reducer)` takes an iterable and applies a function `reducer()` to reduce the iterable to a single value `accumulator` that represents the iterable. The reduce function takes advantage of a **closure** to keep track of the current value of the `accumulator` as it iterates through the iterable.
The reducer function has this signature: `reducer(accumulator, elem)` where `elem` is the current element in the iterable that is to be reduced into the accumulator.
```go
func Reduce[T any](slice []T, reducer func(T, T) T) T {
	var accumulator T
	for i, elem := range slice {
		if i == 0 {
			accumulator = elem
		} else {
			accumulator = reducer(accumulator, elem)
		}
	}
	return accumulator
}
```
