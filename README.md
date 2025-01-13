# csv.nelua

This is a library written in nelua to work with csv files

## API

### csv.parse_file

This function reads a file and returns a sequence of hashmaps, representing the fields in the csv

`csv.parse_file(file_path: string, delim: facultative(string), header: boolean): (boolean, sequence(hashmap(string, string)), string)`

```lua
require "path.to.csv"

local ok, tbl, err = csv.parse_file("example.csv", nil, true)

assert(ok, err)

for _, row in ipairs(tbl) do
  for k, col in pairs(row) do
    print(k, col)
  end
end
```

#### Parameters

- `file_path`: This is the path to the file you want to be read
- `delim`: This is an optional delimeter to be used to seperate the content into its fields, by default it is `,`
- `header`: This specifies whether the first row of content should be considered as the header assigned to fields, if false, all fields are labelled with col(num) e.g `col1`

#### Return Values

- `ok`: A boolean value, to inform if the operation was succesful
- `tbl`: The sequence of hashmaps
- `err`: In the case ok is `false`, the reason, else an empty string

### csv.parse_string

This function reads a string and returns a sequence of hashmaps, representing the fields in the csv  
Functions the same as [csv.parse_file](#csvparse_file)

`csv.parse_string(content: string, delim: facultative(string), header: boolean): (boolean, sequence(hashmap(string, string)), string)`

```lua
require "path.to.csv"

local ok, tbl, err = csv.parse_string("1,2,3\n4,5,6", nil, false)

assert(ok, err)

for _, row in ipairs(tbl) do
  for k, col in pairs(row) do
    print(k, col)
  end
end
```
### csv.encode

This function reads a file and returns a sequence of hashmaps, representing the fields in the csv

`csv.encode(tbl: span(span(string)), delim: facultative(string)): (boolean, string, string)`

```lua
require "path.to.csv"

local tbl: sequence(span(string))
local row1: []string = {"1","2","3"}
local row2: []string = {"4","5","6"}
tbl:push(row1)
tbl:push(row2)

local ok, str, err = csv.encode(tbl, nil)

assert(ok, err)

print(str)
```

#### Parameters

- `tbl`: A span of spans of strings that will be encoded
- `delim`: This is an optional delimeter to be used to seperate the content during encoding, by default it is `,`

#### Return Values

- `ok`: A boolean value, to inform if the operation was succesful
- `str`: The encoded string
- `err`: In the case ok is `false`, the reason, else an empty string
