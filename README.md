# Subjects Extension Specification

- **Title:** Subjects
- **Identifier:** <https://stac-extensions.github.io/subjects/v1.0.0/schema.json>
- **Field Name Prefix:** subjects
- **Scope:** Item, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Proposal
- **Owner**: @emmanuelmathot

This document explains the Subjects Extension to the [SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.
This extension is meant to support using free and normalized keywords. particulary useful when searching for datasets within catalogs with free terms and subjects but also with normalized definition (e.g. geonames).
This extension is inspired by the implementation made by [resto metadata catalog](https://github.com/jjrom/resto).

- Examples:
  - [Item example](examples/item.json): Shows the basic usage of the extension in a STAC Item
<!--  - [Collection example](examples/collection.json): Shows the basic usage of the extension in a STAC Collection
- [JSON Schema](json-schema/schema.json)
- [Changelog](./CHANGELOG.md) -->

## Item Properties and Collection Fields

| Field Name        | Type                        | Description                                          |
| ----------------- | --------------------------- | ---------------------------------------------------- |
| subjects:keywords | [string]                    | List of free keywords associated with the item       |
| Subjects:terms    | [Term Object](#term-object) | A Term Object defining the list of associated terms. |

One of the 2 above fields is REQUIRED.

### Additional Field Information

#### subjects:keywords

The field `subjects:keywords` is open to any names or tag that are relevant to the item.

```json
  "subjects:keywords": ["europe", "france", "paris"]
```
  
### Term Object

The Term Object aim at defining a normalized list of terms based on a documented referencial (e.g. geonames).
Each term has a unique identifier reprensenting its reference system and the term's identifier in that system.

| Field Name | Type   | Description                                                                                                                        |
| ---------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------- |
| id         | string | **REQUIRED**. Unique identifier of the term following the naming convention defined in section [Term identifier](#term-identifier) |
| name       | string | Describe with a huiman readable word the term. Preferably, the same as in the reference system.                                    |
| parentId   | string | Reference a parent term in case of hierarchical relationahip. See section                                                          |

#### Term identifier

The field `id` specifies the term identifier as a `string` that follows the following naming convention:

```
  <system_id>::<id>
```

For instance, the term 

```
  geonames::935877
```

is a term from the [GeoNames geographical database](https://www.geonames.org/) representing the [`Piton de la Fournaise`](https://www.geonames.org/935877).

The list of supported systems is defined in the section Terms Reference Systems.

#### Hierarchical relationship

The field `parent_id` in the Term Object is used to define a hierarchical relationship between terms.

Example, hierarchy of Zurich, Switzerland, Europe: http://api.geonames.org/hierarchy?geonameId=2657896&username=demo

## Terms Reference Systems

  | System    | Prefix     | Description                           |
  | --------- | ---------- | ------------------------------------- |
  | GeoNames  | `geonames` | [Geonames](https://www.geonames.org)  |
  | Wikipedia | `wiki`     | [Wikipedia](https://en.wikipedia.org) |

## Contributing

All contributions are subject to the
[STAC Specification Code of Conduct](https://github.com/radiantearth/stac-spec/blob/master/CODE_OF_CONDUCT.md).
For contributions, please follow the
[STAC specification contributing guide](https://github.com/radiantearth/stac-spec/blob/master/CONTRIBUTING.md) Instructions
for running tests are copied here for convenience.

### Running tests

The same checks that run as checks on PR's are part of the repository and can be run locally to verify that changes are valid. 
To run tests locally, you'll need `npm`, which is a standard part of any [node.js installation](https://nodejs.org/en/download/).

First you'll need to install everything with npm once. Just navigate to the root of this repository and on 
your command line run:
```bash
npm install
```

Then to check markdown formatting and test the examples against the JSON schema, you can run:
```bash
npm test
```

This will spit out the same texts that you see online, and you can then go and fix your markdown or examples.

If the tests reveal formatting problems with the examples, you can fix them with:
```bash
npm run format-examples
```
