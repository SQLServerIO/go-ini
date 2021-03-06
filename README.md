go-ini
======

INI parsing library for Go (golang).

View the API documentation [here](http://godoc.org/github.com/dombenson/go-ini).

Usage
-----

Parse an INI file:

```go
import "github.com/dombenson/go-ini"

file, err := ini.LoadFile("myfile.ini")
```

Get (string) data from the parsed file:

```go
name, ok := file.Get("person", "name")
if !ok {
  panic("'name' variable missing from 'person' section")
}
```

Get (array) data from the parsed file:

```go
colours, ok := file.GetArr("apples", "colour")
if !ok {
  panic("'colours' array variable missing from 'apples' section")
}
```

Iterate through values in a section:

```go
for key, value := range file["mysection"].StringValues() {
  fmt.Printf("%s => %s\n", key, value)
}
```

Iterate through sections in a file:

```go
for name, section := range file {
  fmt.Printf("Section name: %s\n", name)
}
```

Set a value in the file:

```go
file.Set("person", "name", "fred")
```

Write a file out:

```go
file.WriteFile("newfile.ini")
```

File Format
-----------

INI files are parsed by go-ini line-by-line. Each line may be one of the following:

  * A section definition: [section-name]
  * A property: key = value
  * An array property: key[] = value
  * A comment: #blahblah _or_ ;blahblah
  * Blank. The line will be ignored.

Properties defined before any section headers are placed in the default section, which has
the empty string as it's key.

Example:

```ini
# I am a comment
; So am I!

[apples]
colour[] = red
colour[] = green
shape = applish

[oranges]
shape = square
colour = blue
```
