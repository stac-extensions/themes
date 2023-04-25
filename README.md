# Themes Extension Specification

- **Title:** Themes
- **Identifier:** <https://stac-extensions.github.io/themes/v0.0.1/schema.json>
- **Field Name Prefix:** -
- **Scope:** Item, Catalog, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Proposal
- **Owner**: @emmanuelmathot @m-mohr

This document explains the Themes Extension to the [SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.
This extension is meant to support knowledge organization systems used to classify the resource
(i.e. controlled vocabularies / keywords such as [Geonames](https://www.geonames.org) or [Wikipedia](https://en.wikipedia.org)).
If you just need "uncontrolled" free-form keywords / tags, please use the
[`keywords` field](https://github.com/radiantearth/stac-spec/blob/main/item-spec/common-metadata.md#basics) instead.
This extension is based on the field `themes` as defined in [OGC API - Records](https://github.com/opengeospatial/ogcapi-records).

- Examples:
  - [Item example](examples/item.json): Shows the basic usage of the extension in a STAC Item
  - [Collection example](examples/collection.json): Shows the basic usage of the extension in a STAC Collection
- [JSON Schema](json-schema/schema.json)
- [Changelog](./CHANGELOG.md)

## Fields

The fields in the table below can be used in these parts of STAC documents:
- [x] Catalogs
- [x] Collections
- [x] Item Properties (incl. Summaries in Collections)
- [ ] Assets (for both Collections and Items, incl. Item Asset Definitions in Collections)
- [ ] Links

| Field Name | Type                             | Description |
| ---------- | -------------------------------- | ----------- |
| themes     | \[[Theme Object](#theme-object)]] | **REQUIRED.** A knowledge organization system used to classify the STAC entity. Each element is a concept and their respective knowledge organization system / controlled vocabulary. |
  
### Theme Object

The Theme Object aims at defining a normalized list of concepts based on a knowledge organization system / controlled vocabulary (e.g. geonames).

| Field Name | Type                                  | Description |
| ---------- | ------------------------------------- | ----------- |
| concepts   | \[[Concept Object](#concept-object)] | **REQUIRED**. One or more entity/concept identifers from this knowledge system. |
| scheme     | string                                | **REQUIRED**. An identifier for the knowledge organization system used. It is recommended that the identifier is a resolvable URI. |

### Concept Object

Describes an individual concept from the knowledge system.

| Field Name  | Type   | Description |
| ----------- | ------ | ----------- |
| id          | string | **REQUIRED**. An identifier for the concept. |
| title       | string | A human readable title for the concept. |
| description | string | A human readable description for the concept. |
| url         | string | *RECOMMENDED.* A URI providing further description of the concept. |

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
