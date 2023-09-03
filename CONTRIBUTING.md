## Contributing to `bibliodata`
### Scope
The data contained in this repository only includes libraries, and their respective library services, located within the boundaries of [Greater Melbourne](https://www.sro.vic.gov.au/greater-melbourne-map-and-urban-zones), as of the year 2023.

## File format & extension
The file format used for all files within the `data/` folder in this repository _must_ be in YAML, for readability when manually entering data. All data in this folder _must_ have the extension of `.library.yml`.

## File naming
When naming each file, you must either do one of the following:
- On the topic when a library service is named after the council, use the _council name_. (e.g. `moreland.library.yml`, `hobsonsbay.library.yml`)
- If a library service is a regional service, you must **abbreviate the full name of the service**. (e.g. `yprl.library.yml` for Yarra Plenty Regional Library, `erl.library.yml` for Eastern Regional Libraries)

## Schema
Each data file follows a strict [JSON schema](https://json-schema.org/), located in `schema/bibliodata.json`.
### Schema in editors
- If you are using **Visual Studio Code**, the required configuration has already been set up for you, it will already provide the type hints, as well as error-checking.
- If you are using **Neovim**: The plugin [SchemaStore.nvim](https://github.com/b0o/SchemaStore.nvim) will help you, as it supports both JSON and YAML.
Any other editor may need to refer to the relevant guide.
### Field Description
`name`: Name of the library service. (`string`)

`lga`: Names of the [local government areas](https://en.wikipedia.org/wiki/Local_government_in_Australia) that the library operates in. (`array[string]`) <!-- TODO: make this an array | string-->

`site`: Homepage of the library service (`url`)

`libraries`: A list of `library` objects. (`array[Library]`)
### Types
`url`: A valid URL in a `string`.
```yml
url: https://google.com # valid
url: google.com # invalid
```

`coordinate`: A valid coordinate as a floating point number.
```yml
lat: -37.5152576
lng: 145.1227105
```

`Library`: 
- `name`: Official place name of the library. (`string`)

- `suburb`: The suburb that the library is located in. (`string`)

- `lga`: The local government area that the library is located in. (`string`)

- `site`: The page provided by the library service of the branch. (`url`)

- `lat`: The latitude of the location of the library. (`coordinate`)

- `lng`: The longitude of the location of the library. (`coordinate`)


## Converting to GeoJSON
There is a script that iterates over the data folder, to create a GeoJSON-compatible file. To use it, you need to use the following command:
```
$ ./biblioconvert -i data/ -o libraries.geojson
```
This script requires Python 3.5+ and the `geojson` library installed through either `pip` or the system package manager. If you are on Windows, you can also run:
```
python biblioconvert -i data/ -o libraries.geojson
```