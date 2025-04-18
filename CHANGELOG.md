# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).


## [Unreleased]

### Added
- Support for model import from parquet file metadata.

### Changed

### Fixed
- raise valid exception in DataContractSpecification.from_file if file does not exist

## [0.10.14] - 2024-10-26

Data Contract CLI now supports the Open Data Contract Standard (ODCS) v3.0.0.

### Added
- `datacontract test` now also supports ODCS v3 data contract format
- `datacontract export --format odcs_v3`: Export to Open Data Contract Standard v3.0.0 (#460)
- `datacontract test` now also supports ODCS v3 anda Data Contract SQL quality checks on field and model level
- Support for import from Iceberg table definitions.
- Support for decimal logical type on avro export.
- Support for custom Trino types

### Changed
- `datacontract import --format odcs`: Now supports ODSC v3.0.0 files (#474)
- `datacontract export --format odcs`: Now creates v3.0.0 Open Data Contract Standard files (alias to odcs_v3). Old versions are still available as format `odcs_v2`. (#460)

### Fixed
- fix timestamp serialization from parquet -> duckdb (#472)


## [0.10.13] - 2024-09-20

### Added
- `datacontract export --format data-caterer`: Export to [Data Caterer YAML](https://data.catering/setup/guide/scenario/data-generation/)

### Changed
- `datacontract export --format jsonschema` handle optional and nullable fields (#409)
- `datacontract import --format unity` handle nested and complex fields (#420)
- `datacontract import --format spark` handle field descriptions (#420)
- `datacontract export --format bigquery` handle bigqueryType (#422)

### Fixed
- use correct float type with bigquery (#417)
- Support DATACONTRACT_MANAGER_API_KEY
- Some minor bug fixes

## [0.10.12] - 2024-09-08

### Added
- Support for import of DBML Models (#379)
- `datacontract export --format sqlalchemy`: Export to [SQLAlchemy ORM models](https://docs.sqlalchemy.org/en/20/orm/quickstart.html) (#399)
- Support of varchar max length in Glue import (#351)
- `datacontract publish` now also accepts the `DATACONTRACT_MANAGER_API_KEY` as an environment variable
- Support required fields for Avro schema export (#390)
- Support data type map in Spark import and export (#408)
- Support of enum on export to avro
- Support of enum title on avro import

### Changed
- Deltalake is now using DuckDB's native deltalake support (#258). Extra deltalake removed.
- When dumping to YAML (import) the alias name is used instead of the pythonic name. (#373)

### Fixed
- Fix an issue where the datacontract cli fails if installed without any extras (#400)
- Fix an issue where Glue database without a location creates invalid data contract (#351)
- Fix bigint -> long data type mapping (#351)
- Fix an issue where column description for Glue partition key column is ignored (#351)
- Corrected name of table parameter for bigquery import (#377)
- Fix a failed to connect to S3 Server (#384)
- Fix a model bug mismatching with the specification (`definitions.fields`) (#375)
- Fix array type management in Spark import (#408)


## [0.10.11] - 2024-08-08

### Added

- Support data type map in Glue import. (#340)
- Basic html export for new `keys` and `values` fields
- Support for recognition of 1 to 1 relationships when exporting to DBML
- Added support for arrays in JSON schema import (#305)

### Changed

- Aligned JSON schema import and export of required properties
- Change dbt importer to be more robust and customizable

### Fixed

- Fix required field handling in JSON schema import
- Fix an issue where the quality and definition `$ref` are not always resolved
- Fix an issue where the JSON schema validation fails for a field with type `string` and format `uuid`
- Fix an issue where common DBML renderers may not be able to parse parts of an exported file


## [0.10.10] - 2024-07-18

### Added
- Add support for dbt manifest file (#104)
- Fix import of pyspark for type-checking when pyspark isn't required as a module (#312)
- Adds support for referencing fields within a definition (#322)
- Add `map` and `enum` type for Avro schema import (#311)

### Fixed
- Fix import of pyspark for type-checking when pyspark isn't required as a module (#312)- `datacontract import --format spark`: Import from Spark tables (#326)
- Fix an issue where specifying `glue_table` as parameter did not filter the tables and instead returned all tables from `source` database (#333)

## [0.10.9] - 2024-07-03

### Added
- Add support for Trino (#278)
- Spark export: add Spark StructType exporter (#277)
- add `--schema` option for the `catalog` and `export` command to provide the schema also locally
- Integrate support into the pre-commit workflow. For further details, please refer to the information provided [here](./README.md#use-with-pre-commit).
- Improved HTML export, supporting links, tags, and more
- Add support for AWS SESSION_TOKEN (#309)

### Changed
- Added array management on HTML export (#299)

### Fixed
- Fix `datacontract import --format jsonschema` when description is missing (#300)
- Fix `datacontract test` with case-sensitive Postgres table names (#310)

## [0.10.8] - 2024-06-19

### Added
- `datacontract serve` start a local web server to provide a REST-API for the commands
- Provide server for sql export for the appropriate schema (#153)
- Add struct and array management to Glue export (#271)

### Changed
- Introduced optional dependencies/extras for significantly faster installation times. (#213)
- Added delta-lake as an additional optional dependency
- support `GOOGLE_APPLICATION_CREDENTIALS` as variable for connecting to bigquery in `datacontract test`
- better support bigqueries `type` attribute, don't assume all imported models are tables
- added initial implementation of an importer from unity catalog (not all data types supported, yet)
- added the importer factory. This refactoring aims to make it easier to create new importers and consequently the growth and maintainability of the project. (#273)

### Fixed
- `datacontract export --format avro` fixed array structure (#243)

## [0.10.7] - 2024-05-31

### Added
- Test data contract against dataframes / temporary views (#175)

### Fixed
- AVRO export: Logical Types should be nested (#233)

## [0.10.6] - 2024-05-29

### Fixed

- Fixed Docker build by removing msodbcsql18 dependency (temporary workaround)

## [0.10.5] - 2024-05-29

### Added
- Added support for `sqlserver` (#196)
- `datacontract export --format dbml`: Export to [Database Markup Language (DBML)](https://dbml.dbdiagram.io/home/) (#135)
- `datacontract export --format avro`: Now supports config map on field level for logicalTypes and default values [Custom Avro Properties](./README.md#custom-avro-properties)
- `datacontract import --format avro`: Now supports importing logicalType and default definition on avro files [Custom Avro Properties](./README.md#custom-avro-properties)
- Support `config.bigqueryType` for testing BigQuery types
- Added support for selecting specific tables in an AWS Glue `import` through the `glue-table` parameter (#122)

### Fixed

- Fixed jsonschema export for models with empty object-typed fields (#218)
- Fixed testing BigQuery tables with BOOL fields
- `datacontract catalog` Show search bar also on mobile

## [0.10.4] - 2024-05-17

### Added

- `datacontract catalog` Search
- `datacontract publish`: Publish the data contract to the Data Mesh Manager
- `datacontract import --format bigquery`: Import from BigQuery format (#110)
- `datacontract export --format bigquery`: Export to BigQuery format (#111)
- `datacontract export --format avro`: Now supports [Avro logical types](https://avro.apache.org/docs/1.11.1/specification/#logical-types) to better model date types. `date`, `timestamp`/`timestamp-tz` and `timestamp-ntz` are now mapped to the appropriate logical types. (#141)
- `datacontract import --format jsonschema`: Import from JSON schema (#91)
- `datacontract export --format jsonschema`: Improved export by exporting more additional information
- `datacontract export --format html`: Added support for Service Levels, Definitions, Examples and nested Fields
- `datacontract export --format go`: Export to go types format

## [0.10.3] - 2024-05-05

### Fixed
- datacontract catalog: Add index.html to manifest

## [0.10.2] - 2024-05-05

### Added

- Added import glue (#166)
- Added test support for `azure` (#146)
- Added support for `delta` tables on S3 (#24)
- Added new command `datacontract catalog` that generates a data contract catalog with an `index.html` file.
- Added field format information to HTML export

### Fixed
- RDF Export: Fix error if owner is not a URI/URN


## [0.10.1] - 2024-04-19

### Fixed

- Fixed docker columns

## [0.10.0] - 2024-04-19

### Added

- Added timestamp when ah HTML export was created

### Fixed

- Fixed export format **html**

## [0.9.9] - 2024-04-18

### Added

- Added export format **html** (#15)
- Added descriptions as comments to `datacontract export --format sql` for Databricks dialects
- Added import of arrays in Avro import

## [0.9.8] - 2024-04-01

### Added

- Added export format **great-expectations**: `datacontract export --format great-expectations`
- Added gRPC support to OpenTelemetry integration for publishing test results
- Added AVRO import support for namespace (#121)
- Added handling for optional fields in avro import (#112)
- Added Databricks SQL dialect for `datacontract export --format sql`

### Fixed

- Use `sql_type_converter` to build checks.
- Fixed AVRO import when doc is missing (#121)

## [0.9.7] - 2024-03-15

### Added

- Added option publish test results to **OpenTelemetry**: `datacontract test --publish-to-opentelemetry`
- Added export format **protobuf**: `datacontract export --format protobuf`
- Added export format **terraform**: `datacontract export --format terraform` (limitation: only works for AWS S3 right now)
- Added export format **sql**: `datacontract export --format sql`
- Added export format **sql-query**: `datacontract export --format sql-query`
- Added export format **avro-idl**: `datacontract export --format avro-idl`: Generates an Avro IDL file containing records for each model.
- Added new command **changelog**: `datacontract changelog datacontract1.yaml datacontract2.yaml` will now generate a changelog based on the changes in the data contract. This will be useful for keeping track of changes in the data contract over time.
- Added extensive linting on data contracts. `datacontract lint` will now check for a variety of possible errors in the data contract, such as missing descriptions, incorrect references to models or fields, nonsensical constraints, and more.
- Added importer for avro schemas. `datacontract import --format avro` will now import avro schemas into a data contract.

### Fixed

- Fixed a bug where the export to YAML always escaped the unicode characters.


## [0.9.6-2] - 2024-03-04

### Added

- test kafka for avro messages
- added export format **avro**: `datacontract export --format avro`

## [0.9.6] - 2024-03-04

This is a huge step forward, we now support testing Kafka messages.
We start with JSON messages and avro, and Protobuf will follow.

### Added
- test kafka for JSON messages
- added import format **sql**: `datacontract import --format sql` (#51)
- added export format **dbt-sources**: `datacontract export --format dbt-sources`
- added export format **dbt-staging-sql**: `datacontract export --format dbt-staging-sql`
- added export format **rdf**: `datacontract export --format rdf` (#52)
- added command `datacontract breaking` to detect breaking changes in between two data contracts.

## [0.9.5] - 2024-02-22

### Added
- export to dbt models (#37).
- export to ODCS (#49).
- test - show a test summary table.
- lint - Support local schema (#46).

## [0.9.4] - 2024-02-18

### Added
- Support for Postgres
- Support for Databricks

## [0.9.3] - 2024-02-10

### Added
- Support for BigQuery data connection
- Support for multiple models with S3

### Fixed

- Fix Docker images. Disable builds for linux/amd64.

## [0.9.2] - 2024-01-31

### Added
- Publish to Docker Hub

## [0.9.0] - 2024-01-26 - BREAKING

This is a breaking change (we are still on a 0.x.x version).
The project migrated from Golang to Python.
The Golang version can be found at [cli-go](https://github.com/datacontract/cli-go)

### Added
- `test` Support to directly run tests and connect to data sources defined in servers section.
- `test` generated schema tests from the model definition.
- `test --publish URL` Publish test results to a server URL.
- `export` now exports the data contract so format jsonschema and sodacl.

### Changed
- The `--file` option removed in favor of a direct argument.: Use `datacontract test datacontract.yaml` instead of `datacontract test --file datacontract.yaml`.

### Removed
- `model` is now part of `export`
- `quality` is now part of `export`
- Temporary Removed: `diff` needs to be migrated to Python.
- Temporary Removed: `breaking` needs to be migrated to Python.
- Temporary Removed: `inline` needs to be migrated to Python.

## [0.6.0]
### Added
- Support local json schema in lint command.
- Update to specification 0.9.2.

## [0.5.3]
### Fixed
- Fix format flag bug in model (print) command.

## [0.5.2]
### Changed
- Log to STDOUT.
- Rename `model` command parameter, `type` -> `format`.

## [0.5.1]
### Removed
- Remove `schema` command.

### Fixed
- Fix documentation.
- Security update of x/sys.

## [0.5.0]
### Added
- Adapt Data Contract Specification in version 0.9.2.
- Use `models` section for `diff`/`breaking`.
- Add `model` command.
- Let `inline` print to STDOUT instead of overwriting datacontract file.
- Let `quality` write input from STDIN if present.

## [0.4.0]
### Added
- Basic implementation of `test` command for Soda Core.

### Changed
- Change package structure to allow usage as library.

## [0.3.2]
### Fixed
- Fix field parsing for dbt models, affects stability of `diff`/`breaking`.

## [0.3.1]
### Fixed
- Fix comparing order of contracts in `diff`/`breaking`.

## [0.3.0]
### Added
- Handle non-existent schema specification when using `diff`/`breaking`.
- Resolve local and remote resources such as schema specifications when using "$ref: ..." notation.
- Implement `schema` command: prints your schema.
- Implement `quality` command: prints your quality definitions.
- Implement the `inline` command: resolves all references using the "$ref: ..." notation and writes them to your data contract.

### Changed
- Allow remote and local location for all data contract inputs (`--file`, `--with`).

## [0.2.0]
### Added
- Add `diff` command for dbt schema specification.
- Add `breaking` command for dbt schema specification.

### Changed
- Suggest a fix during `init` when the file already exists.
- Rename `validate` command to `lint`.

### Removed
- Remove `check-compatibility` command.

### Fixed
- Improve usage documentation.

## [0.1.1]
### Added
- Initial release.
