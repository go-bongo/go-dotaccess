Dot notation set/get. Mainly just a wrapper for github.com/oleiade/reflections, so that should get most of the credit.

Note that for now setting only works on pointers to structs. Getting works on nested structs and nested struct pointers.

Since this is intended to work on public properties, each element in the dot notation string is converted to title case.

# Get
```go
type ChildStruct struct {
	Prop string
}
type MyStruct struct {
	Nested *ChildStruct
}

myStruct := &MyStruct{
	Nested:&ChildStruct{"foo"},
}

// This will get myStruct.Nested.Prop
val, err := dotaccess.Get(myStruct, "nested.prop")
// returns "foo", nil

val, err = dotaccess.Get(myStruct, "foo.bar")
//returns nil, error
```

# Set
```go
err := dotaccess.Set(myStruct, "nested.prop", "bar")

fmt.Println(myStruct.Nested.Prop)
// "bar"
```


