Upgrading from API v3
=====================

## SSL enforced
The API is available only via secure HTTPS.

## Gzip compression
All responses will now utilize compression.

## Organisations are now Service Points
The endpoint `/organisation` has been renamed to `/service_point`. This endpoint can be used to query
libraries, mobile libraries, museums and archives.

```
/service_point
/service_point/{id}
```

The separation between each type is made with property `type`.

For libraries there exists various types. Museums, archives and "anonymous" service points have one
type each.

Type    | Description
------- | -----------
archive | Archive
museum  | Museum
other   | Unspecified type

Available types for libraries are listed on the [main documentation](#fooo).

### Non-service point documents excluded
The endpoint no longer returns other types of documents such as mobile library stops, departments or
so-called meta organisations. Departments and mobile stops are now a property of the library they're
attached to.

### Regarding parameters `type` and `branch_type`
Due to the separation mentioned above, there is no longer need for a property for identifying between
different document types. Therefore the original `type` parameter/property has been dropped, and
`branch_type` has been renamed to `type`.

#### (Branch) types `regional` and `main_library`
The two special types `regional` and `main_library` have been turned into their own parameters in order
to gather all regular municipal libraries under a single type.

### Additional notes
The endpoint no more returns other types of documents such as mobile library stops, departments under
service points or so-called meta organisations.

### Different schemas
Library can be considered as a supertype of the more generic service point. (To be elaborated more.)

## Translations in documents
Whereas the older APIs returned fields for every language supported by the system, form now on only
those languages will be returned for which a translation exists. This means that different documents
(libraries etc.) might contain different sets of languages.

## Libraries
Since the main purpose of the API is to provide access to **libraries**, there is a dedicated endpoint
for querying libraries only.

```
/library
/library/{id}
```

## Library consortiums
### Distinction between library consortiums and Finna organisations
From now on Finna organisations are served from their own endpoint.

Any consortium that is also a Finna organisation will be available on both endpoints, but the data
specific to Finna is available from through `/finna_organisation`.

Any Finna organisation that is NOT a library consortium will not be available through `/consortium`.

## Services
### No more parameter helmet:type_priority
This parameter has been removed. To fetch only services that are available at HelMet libraries, use
parameters `consortium` or `consortium.name`.