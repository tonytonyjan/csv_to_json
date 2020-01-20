# csv_to_json

A command-line tool for converting CSV to JSON

## Installation

```
gem install csv_to_json
```

## Usage

```
$ csv_to_json --help
Usage: csv_to_json [options] [FILE]
        --headers=x,y,z
        --converters=x,y,z
        --[no-]stream
    -h, --help                       Prints this help
```

### Header Detectection

```
$ printf 'name,age,birth\nTony,18,1989-11-23\nJason,19,1919-12-13' |
  csv_to_json | jq
[
  {
    "name": "Tony",
    "age": "18",
    "birth": "1989-11-23"
  },
  {
    "name": "Jason",
    "age": "19",
    "birth": "1919-12-13"
  }
]
```
### Custom Headers

```
$ printf 'Tony,18,1989-11-23\nJason,19,1919-12-13' |
  csv_to_json --headers name,age,birth | jq
[
  {
    "name": "Tony",
    "age": "18",
    "birth": "1989-11-23"
  },
  {
    "name": "Jason",
    "age": "19",
    "birth": "1919-12-13"
  }
]
```

### Type Conversion

```
$ printf 'name,age,birth\nTony,18,1989-11-23\nJason,19,1919-12-13' |
  csv_to_json --converters numeric | jq
[
  {
    "name": "Tony",
    "age": 18,
    "birth": "1989-11-23"
  },
  {
    "name": "Jason",
    "age": 19,
    "birth": "1919-12-13"
  }
]
```

### Streaming

```
$ printf 'name,age,birth\nTony,18,1989-11-23\nJason,19,1919-12-13' |
  csv_to_json --stream
{"name":"Tony","age":"18","birth":"1989-11-23"}
{"name":"Jason","age":"19","birth":"1919-12-13"}
```
