# Cucumber REST Gherkin library

![Java CI with Gradle](https://github.com/Ragin-LundF/bbd-cucumber-gherkin-lib/workflows/Java%20CI%20with%20Gradle/badge.svg)
[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=Ragin-LundF_bbd-cucumber-gherkin-lib&metric=alert_status)](https://sonarcloud.io/dashboard?id=Ragin-LundF_bbd-cucumber-gherkin-lib)

This library supports some basic sentences to handle REST API calls and basic database operations.

It is based on [Cucumber](https://cucumber.io) and helps to support [Behaviour-Driven Development (BDD)](https://cucumber.io/docs/bdd/).

Cucumber executes `Steps` in form of [Gherkin](https://cucumber.io/docs/gherkin/) language.

Read also about [Anti-Patterns](https://cucumber.io/docs/guides/anti-patterns/) of Cucumber to avoid problems and to have a clear style.

See [Changelog](CHANGELOG.md) for release information.

# Table of content

- [Cucumber REST Gherkin library](#cucumber-rest-gherkin-library)
- [Table of content](#table-of-content)
- [Support JUnit 5](#support-junit-5)
- [Basic Concept](#basic-concept)
- [Steps](#steps)
  - [Database](#database)
    - [Given](#given)
      - [Liquibase script initialization](#liquibase-script-initialization)
      - [SQL statement execution](#sql-statement-execution)
    - [Then](#then)
      - [Database data comparision](#database-data-comparision)
  - [REST](#rest)
    - [JSON-Unit](#json-unit)
    - [Given](#given-1)
      - [Set path base directory for request/result/database files](#set-path-base-directory-for-requestresultdatabase-files)
      - [Set base path for URLs](#set-base-path-for-urls)
      - [Define that a token without scopes should be used.](#define-that-a-token-without-scopes-should-be-used)
      - [Set a URI path for later execution](#set-a-uri-path-for-later-execution)
      - [Set a body from JSON file for later execution](#set-a-body-from-json-file-for-later-execution)
      - [Set a body directly for later execution](#set-a-body-directly-for-later-execution)
    - [When](#when)
      - [GET requests](#get-requests)
        - [Execute a GET request call with previously given URI](#execute-a-get-request-call-with-previously-given-uri)
        - [Execute an authorized GET request call with previously given URI](#execute-an-authorized-get-request-call-with-previously-given-uri)
        - [Execute a GET request call to an endpoint](#execute-a-get-request-call-to-an-endpoint)
        - [Execute an authorized GET request call](#execute-an-authorized-get-request-call)
        - [Execute an authorized GET request call to previously given URL with dynamic URI elements](#execute-an-authorized-get-request-call-to-previously-given-url-with-dynamic-uri-elements)
        - [Execute a GET request call to previously given URL with dynamic URI elements](#execute-a-get-request-call-to-previously-given-url-with-dynamic-uri-elements)
      - [POST requests](#post-requests)
        - [Execute a POST request to an endpoint with previously given URI and body](#execute-a-post-request-to-an-endpoint-with-previously-given-uri-and-body)
        - [Execute an authorized POST request call to an endpoint with previously given URI and body](#execute-an-authorized-post-request-call-to-an-endpoint-with-previously-given-uri-and-body)
        - [Execute a POST request call to a URL with a previously given body](#execute-a-post-request-call-to-a-url-with-a-previously-given-body)
        - [Execute an authorized POST request call to a URL with a previously given body](#execute-an-authorized-post-request-call-to-a-url-with-a-previously-given-body)
        - [Execute a POST request call to an endpoint with body from file](#execute-a-post-request-call-to-an-endpoint-with-body-from-file)
        - [Execute an authorized POST request call to an endpoint with body from file](#execute-an-authorized-post-request-call-to-an-endpoint-with-body-from-file)
        - [Execute an authorized POST request call to previously given URL and body with dynamic URI elements](#execute-an-authorized-post-request-call-to-previously-given-url-and-body-with-dynamic-uri-elements)
        - [Execute a POST request call to previously given URL and body with dynamic URI elements](#execute-a-post-request-call-to-previously-given-url-and-body-with-dynamic-uri-elements)
      - [PUT requests](#put-requests)
        - [Execute a PUT request to an endpoint with previously given URI and body](#execute-a-put-request-to-an-endpoint-with-previously-given-uri-and-body)
        - [Execute an authorized PUT request call to an endpoint with previously given URI and body](#execute-an-authorized-put-request-call-to-an-endpoint-with-previously-given-uri-and-body)
        - [Execute a PUT request call to a URL with a previously given body](#execute-a-put-request-call-to-a-url-with-a-previously-given-body)
        - [Execute an authorized PUT request call to a URL with a previously given body](#execute-an-authorized-put-request-call-to-a-url-with-a-previously-given-body)
        - [Execute a PUT request call to an endpoint with body from file](#execute-a-put-request-call-to-an-endpoint-with-body-from-file)
        - [Execute an authorized PUT request call to an endpoint with body from file](#execute-an-authorized-put-request-call-to-an-endpoint-with-body-from-file)
        - [Execute an authorized PUT request call to previously given URL and body with dynamic URI elements](#execute-an-authorized-put-request-call-to-previously-given-url-and-body-with-dynamic-uri-elements)
        - [Execute a PUT request call to previously given URL and body with dynamic URI elements](#execute-a-put-request-call-to-previously-given-url-and-body-with-dynamic-uri-elements)
      - [PATCH requests](#patch-requests)
        - [Execute a PATCH request to an endpoint with previously given URI and body](#execute-a-patch-request-to-an-endpoint-with-previously-given-uri-and-body)
        - [Execute an authorized PATCH request call to an endpoint with previously given URI and body](#execute-an-authorized-patch-request-call-to-an-endpoint-with-previously-given-uri-and-body)
        - [Execute a PATCH request call to a URL with a previously given body](#execute-a-patch-request-call-to-a-url-with-a-previously-given-body)
        - [Execute an authorized PATCH request call to a URL with a previously given body](#execute-an-authorized-patch-request-call-to-a-url-with-a-previously-given-body)
        - [Execute a PATCH request call to an endpoint with body from file](#execute-a-patch-request-call-to-an-endpoint-with-body-from-file)
        - [Execute an authorized PATCH request call to an endpoint with body from file](#execute-an-authorized-patch-request-call-to-an-endpoint-with-body-from-file)
        - [Execute an authorized PATCH request call to previously given URL and body with dynamic URI elements](#execute-an-authorized-patch-request-call-to-previously-given-url-and-body-with-dynamic-uri-elements)
        - [Execute a PATCH request call to previously given URL and body with dynamic URI elements](#execute-a-patch-request-call-to-previously-given-url-and-body-with-dynamic-uri-elements)
      - [DELETE requests](#delete-requests)
        - [Execute a DELETE request to an endpoint with previously given URI and body](#execute-a-delete-request-to-an-endpoint-with-previously-given-uri-and-body)
        - [Execute an authorized DELETE request call to an endpoint with previously given URI and body](#execute-an-authorized-delete-request-call-to-an-endpoint-with-previously-given-uri-and-body)
        - [Execute a DELETE request call to a URL with a previously given body](#execute-a-delete-request-call-to-a-url-with-a-previously-given-body)
        - [Execute an authorized DELETE request call to a URL with a previously given body](#execute-an-authorized-delete-request-call-to-a-url-with-a-previously-given-body)
        - [Execute a DELETE request call to an endpoint with body from file](#execute-a-delete-request-call-to-an-endpoint-with-body-from-file)
        - [Execute an authorized DELETE request call to an endpoint with body from file](#execute-an-authorized-delete-request-call-to-an-endpoint-with-body-from-file)
        - [Execute an authorized DELETE request call to previously given URL and body with dynamic URI elements](#execute-an-authorized-delete-request-call-to-previously-given-url-and-body-with-dynamic-uri-elements)
        - [Execute a DELETE request call to previously given URL and body with dynamic URI elements](#execute-a-delete-request-call-to-previously-given-url-and-body-with-dynamic-uri-elements)
      - [Body manipulation](#body-manipulation)
    - [Then](#then-1)
      - [Validate HTTP response code](#validate-http-response-code)
      - [Validate response body with JSON file](#validate-response-body-with-json-file)
      - [Validate response body with given String](#validate-response-body-with-given-string)
      - [Read from Response and set it to a `Feature` context](#read-from-response-and-set-it-to-a-feature-context)
- [Extension of JSON Unit Matcher](#extension-of-json-unit-matcher)
  - [Simple matcher](#simple-matcher)
  - [Matcher with parameter](#matcher-with-parameter)
  
# Support JUnit 5
To support JUnit 5 add the `org.junit.vintage:junit-vintage-engine` dependency to your project.
This allows JUnit 5 to execute JUnit 3 and 4 tests.

```groovy
testRuntimeOnly('org.junit.vintage:junit-vintage-engine') {
    because("allows JUnit 3 and JUnit 4 tests to run")
}
```

# Basic Concept

This library defines a set of sentences and tries to harmonize them and provide a context-related beginning of sentences.
This is very helpful for IDEs with code completion.

| Step | Sentence start | Main usage |
| --- | --- | --- |
| `Given` | `that` | Prepare something |
| `When` | `executing a` or `I set` | Do something |
| `Then` | `I ensure` or `I store` | Validate something |

There are some basic examples in the [src/test](src/test) directory.

# Steps
It is a best-practice to not use syntax like this:
```gherkin
Scenario:
  Given that something was done
  Given that something else was done
  Given that something more was done
```

For that `Gherkin` offers `Steps` like `And` to make the definition more readable. In general every sentence can be reused with another `Step`.
It is recommended to follow the basic definition like described under [Basic concept](#basic-concept).

This transforms the upper example to:
```gherkin
Scenario:
  Given that something was done
  And that something else was done
  And that something more was done
```

This sounds much better, didn't it?


## Database
Before every Scenario the library looks for a `database/reset_database.xml` file (`$projectDir/src/test/resources/database/reset_database.xml`).
This file has to be a [Liquibase](https://www.liquibase.org) definition, which can contain everything to reset a database (`truncate`, `delete`, `insert`...).

### Given
#### Liquibase script initialization
```gherkin
Scenario:
  Given that the database was initialized with the liquibase file {string}
```

Executes a liquibase script to prepare the database.

#### SQL statement execution
```gherkin
Scenario:
    Given that the SQL statements from the SQL file {string} was executed
```

Executes an SQL script to prepare/change the database.

### Then
#### Database data comparision
```gherkin
Scenario:
  Then I ensure that the result of the query of the file {string} is equal to the CSV file {string}
```

Executes an SQL query from a file and compares the result in CSV format with the contents of the second file.
The conversion of the database result to CSV is done internally.

## REST
The REST API steps can be prepared with some given steps.

### JSON-Unit

The library contains already two matchers:
- `${json-unit.matches:isValidDate}` which checks, if the date can be a valid date by parsing it into date formats
- `${json-unit.matches:isEqualToScenarioContext}create_id` which compares the content of the actual JSON to a variable in the ScenarioContext.
  The context has to be set before with the [I store the string of the field "<field>" in the context "<context-id>" for later usage](#read-from-response-and-set-it-to-a-feature-context) sentence.

There are more details about how to extend it at the [Extension of JSON Unit Matcher](#extension-of-json-unit-matcher) section.

For the comparison of the results the library uses `JSON` files, which can be enhanced with [JSON Unit](https://github.com/lukas-krecan/JsonUnit) to validate dynamic responses with things like
- Regex compare
- Ignoring values
- Ignoring elements
- Ignoring paths
- Type placeholders
- Custom matchers
- ...

### Given
#### Set path base directory for request/result/database files
```gherkin
Scenario:
  Given that all file paths are relative to {string}
```

Sets an internal `base file path` for all files in the `Scenario` or `Feature`.
It is used for:
- Request files
- Response files (for compare)
- Database query files (`.sql`)
- Database CSV result files (`.csv`)

#### Set base path for URLs
```gherkin
Scenario:
  Given that all URLs are relative to {string}
```

Sets an internal `base URL path` for all URLs in the `Scenario` or `Feature`.
This is very useful to avoid repeating e.g. `/api/v1/myapitotest` before every concrete endpoint.

#### Define that a token without scopes should be used.
```gherkin
Scenario:
  Given that a bearer token without scopes is used
```

This library supports two types of Bearer tokens. With this step it possible to set the token without scope.
Else it uses the default token, which should contain correct `scopes`/`authorities`.

The token has to be configured in the `application.yml` / `application.properties` in the `src/main/test/resources` directory.

The token can be set like:

`application.properties`:
```properties
cucumberTest.authorization.bearerToken.noscope=eyJhbGciOiJI[...]V_adQssw5c
cucumberTest.authorization.bearerToken.default=eyJfgEiooIfS[...]Bs_sadf4de
```

`application.yml`:
```yaml
cucumberTest:
  authorization:
    bearerToken:
      noscope: eyJhbGciOiJI[...]V_adQssw5c
      default: eyJfgEiooIfS[...]Bs_sadf4de
```

#### Set a URI path for later execution
```gherkin
Scenario:
  Given that the API path is {string}
```
This sets a URI, path which can be executed later.
It is required to use this `Given`/`And` step in cases when it is necessary to manipulate e.g. dynamic elements in the URI.

#### Set a body from JSON file for later execution
```gherkin
Scenario:
  Given that the file {string} is used as the body
```

This sets the JSON file for the body for later execution.
It is required to use this `Given` step in cases when it is necessary to manipulate e.g. dynamic elements in the URI.

#### Set a body directly for later execution
```gherkin
Scenario:
  Given that the body of the response is
    """
    {
      "key": "value"
    }
    """
```

This sets the JSON body for later execution.
It is required to use this `Given` step in cases when it is necessary to manipulate e.g. dynamic elements in the URI.


### When
The paths that are used here can be shortened by set a base URL path with [Set base path for URLs](#set-base-path-for-urls) with a `Given` Step before.

#### GET requests
##### Execute a GET request call with previously given URI
```gherkin
Scenario:
  When executing a GET call with previously given URI
```

Calls a previously given URL path as a `GET` request without `Authorization` header.

##### Execute an authorized GET request call with previously given URI
```gherkin
Scenario:
  When executing an authorized GET call with previously given URI
```

Calls a previously given URL path as a `GET` request with `Authorization` header.

##### Execute a GET request call to an endpoint
```gherkin
Scenario:
  When executing a GET call to {string}
```

Calls the given URL path as a `GET` request without `Authorization` header.

##### Execute an authorized GET request call
```gherkin
Scenario:
  When executing an authorized GET call to {string}
```

Calls the given URL path as a `GET` request with `Authorization` header and `Bearer` token.
The used token depends on [Define that a token without scopes should be used](#define-that-a-token-without-scopes-should-be-used) `Step`.


##### Execute an authorized GET request call to previously given URL with dynamic URI elements
```gherkin
Scenario:
  When executing an authorized GET call with previously given API path and these dynamic 'URI Elements' replaced with the 'URI Values'
    | URI Elements  | URI Values |
    | resourceId    | abc-def-gh |
    | subResourceId | abc-def-gh |
```

Calls a previously given URL path as a `GET` request and replace dynamic URI elements with values.

In the example above the given link looks like: `/api/v1/endpoint/{resourceId}/{subResourceId}`.
The dynamic elements `{resourceId}` and `{subResourceId}` will be replaced with the values from the datatable below the sentence.

This datatable requires the header `| URI Elements  | URI Values |`.

The values do first a lookup in the `ScenarioStateContext`, if there is a key equal to the `URI Values` value.
If it finds the key, this key will be used, else it uses the value of the table directly.

To set something to the `ScenarioStateContext` it is possible to use [Read from Response and set it to a Feature context](#read-from-response-and-set-it-to-a-feature-context).
But like mentioned at this point, this is an [Anti-Pattern](https://cucumber.io/docs/guides/anti-patterns/), which should be used with caution.

**Requires the `Step` [Set a URI path for later execution](#set-a-uri-path-for-later-execution)!**
The used token depends on [Define that a token without scopes should be used](#define-that-a-token-without-scopes-should-be-used) `Step`.


##### Execute a GET request call to previously given URL with dynamic URI elements
```gherkin
Scenario:
  When executing a GET call with previously given API path and these dynamic 'URI Elements' replaced with the 'URI Values'
    | URI Elements  | URI Values |
    | resourceId    | abc-def-gh |
    | subResourceId | abc-def-gh |
```

Calls a previously given URL path as a `GET` request and replace dynamic URI elements with values.

In the example above the given link looks like: `/api/v1/endpoint/{resourceId}/{subResourceId}`.
The dynamic elements `{resourceId}` and `{subResourceId}` will be replaced with the values from the datatable below the sentence.

This datatable requires the header `| URI Elements  | URI Values |`.

The values do first a lookup in the `ScenarioStateContext`, if there is a key equal to the `URI Values` value.
If it finds the key, this key will be used, else it uses the value of the table directly.

To set something to the `ScenarioStateContext` it is possible to use [Read from Response and set it to a Feature context](#read-from-response-and-set-it-to-a-feature-context).
But like mentioned at this point, this is an [Anti-Pattern](https://cucumber.io/docs/guides/anti-patterns/), which should be used with caution.

**Requires the `Step` [Set a URI path for later execution](#set-a-uri-path-for-later-execution)!**


#### POST requests
##### Execute a POST request to an endpoint with previously given URI and body
```gherkin
Scenario:
  When executing a POST call with previously given URI and body
```

Calls a previously given URI path as a `POST` request without `Authorization` header, and a previously given body.

##### Execute an authorized POST request call to an endpoint with previously given URI and body
```gherkin
Scenario:
  When executing an authorized POST call with previously given URI and body
```

Calls a previously given URL path as a `POST` request with `Authorization` header, and a previously given body.

##### Execute a POST request call to a URL with a previously given body
```gherkin
Scenario:
  When executing a POST call to {string} with previously given body
```

Calls the given URL path with a previously given Body as a `POST` request.

##### Execute an authorized POST request call to a URL with a previously given body
```gherkin
Scenario:
  When executing an authorized POST call to {string} with previously given body
```

Calls the given URL path with a previously given Body as a `POST` request.

The used token depends on [Define that a token without scopes should be used](#define-that-a-token-without-scopes-should-be-used) `Step`.


##### Execute a POST request call to an endpoint with body from file
```gherkin
Scenario:
  When executing a POST call to {string} with the body from file {string}
```

Calls the given URL path as a `POST` request without `Authorization` header, and a body defined in the given file.

##### Execute an authorized POST request call to an endpoint with body from file
```gherkin
Scenario:
  When executing an authorized POST call to {string} with the body from file {string}
```

Calls the given URL path as a `POST` request with `Authorization` header, and a body defined in the given file.
The used token depends on [Define that a token without scopes should be used](#define-that-a-token-without-scopes-should-be-used) `Step`.

##### Execute an authorized POST request call to previously given URL and body with dynamic URI elements
```gherkin
Scenario:
  When executing an authorized POST call with previously given API path, body and these dynamic 'URI Elements' replaced with the 'URI Values'
    | URI Elements  | URI Values |
    | resourceId    | abc-def-gh |
    | subResourceId | abc-def-gh |
```

Calls a previously given URL path and Body as a `POST` request and replace dynamic URI elements with values.

In the example above the given link looks like: `/api/v1/endpoint/{resourceId}/{subResourceId}`.
The dynamic elements `{resourceId}` and `{subResourceId}` will be replaced with the values from the datatable below the sentence.

This datatable requires the header `| URI Elements  | URI Values |`.

The values do first a lookup in the `ScenarioStateContext`, if there is a key equal to the `URI Values` value.
If it finds the key, this key will be used, else it uses the value of the table directly.

To set something to the `ScenarioStateContext` it is possible to use [Read from Response and set it to a Feature context](#read-from-response-and-set-it-to-a-feature-context).
But like mentioned at this point, this is an [Anti-Pattern](https://cucumber.io/docs/guides/anti-patterns/), which should be used with caution.

**Requires the `Steps` [Set a URI path for later execution](#set-a-uri-path-for-later-execution) and [Set a body from JSON file for later execution](#set-a-body-from-json-file-for-later-execution)!**
The used token depends on [Define that a token without scopes should be used](#define-that-a-token-without-scopes-should-be-used) `Step`.

##### Execute a POST request call to previously given URL and body with dynamic URI elements
```gherkin
Scenario:
  When executing a POST call with previously given API path, body and these dynamic 'URI Elements' replaced with the 'URI Values'
    | URI Elements  | URI Values |
    | resourceId    | abc-def-gh |
    | subResourceId | abc-def-gh |
```

Calls a previously given URL path and Body as a `POST` request and replace dynamic URI elements with values.

In the example above the given link looks like: `/api/v1/endpoint/{resourceId}/{subResourceId}`.
The dynamic elements `{resourceId}` and `{subResourceId}` will be replaced with the values from the datatable below the sentence.

This datatable requires the header `| URI Elements  | URI Values |`.

The values do first a lookup in the `ScenarioStateContext`, if there is a key equal to the `URI Values` value.
If it finds the key, this key will be used, else it uses the value of the table directly.

To set something to the `ScenarioStateContext` it is possible to use [Read from Response and set it to a Feature context](#read-from-response-and-set-it-to-a-feature-context).
But like mentioned at this point, this is an [Anti-Pattern](https://cucumber.io/docs/guides/anti-patterns/), which should be used with caution.

**Requires the `Steps` [Set a URI path for later execution](#set-a-uri-path-for-later-execution) and [Set a body from JSON file for later execution](#set-a-body-from-json-file-for-later-execution)!**


#### PUT requests
##### Execute a PUT request to an endpoint with previously given URI and body
```gherkin
Scenario:
  When executing a PUT call with previously given URI and body
```

Calls a previously given URI path as a `PUT` request without `Authorization` header, and a previously given body.

##### Execute an authorized PUT request call to an endpoint with previously given URI and body
```gherkin
Scenario:
  When executing an authorized PUT call with previously given URI and body
```

Calls a previously given URL path as a `PUT` request with `Authorization` header, and a previously given body.

##### Execute a PUT request call to a URL with a previously given body
```gherkin
Scenario:
  When executing a PUT call to {string} with previously given body
```

Calls the given URL path with a previously given Body as a `PUT` request.

##### Execute an authorized PUT request call to a URL with a previously given body
```gherkin
Scenario:
  When executing an authorized PUT call to {string} with previously given body
```

Calls the given URL path with a previously given Body as a `PUT` request.

The used token depends on [Define that a token without scopes should be used](#define-that-a-token-without-scopes-should-be-used) `Step`.


##### Execute a PUT request call to an endpoint with body from file
```gherkin
Scenario:
  When executing a PUT call to {string} with the body from file {string}
```

Calls the given URL path as a `PUT` request without `Authorization` header, and a body defined in the given file.

##### Execute an authorized PUT request call to an endpoint with body from file
```gherkin
Scenario:
  When executing an authorized PUT call to {string} with the body from file {string}
```

Calls the given URL path as a `PUT` request with `Authorization` header, and a body defined in the given file.
The used token depends on [Define that a token without scopes should be used](#define-that-a-token-without-scopes-should-be-used) `Step`.

##### Execute an authorized PUT request call to previously given URL and body with dynamic URI elements
```gherkin
Scenario:
  When executing an authorized PUT call with previously given API path, body and these dynamic 'URI Elements' replaced with the 'URI Values'
    | URI Elements  | URI Values |
    | resourceId    | abc-def-gh |
    | subResourceId | abc-def-gh |
```

Calls a previously given URL path and Body as a `PUT` request and replace dynamic URI elements with values.

In the example above the given link looks like: `/api/v1/endpoint/{resourceId}/{subResourceId}`.
The dynamic elements `{resourceId}` and `{subResourceId}` will be replaced with the values from the datatable below the sentence.

This datatable requires the header `| URI Elements  | URI Values |`.

The values do first a lookup in the `ScenarioStateContext`, if there is a key equal to the `URI Values` value.
If it finds the key, this key will be used, else it uses the value of the table directly.

To set something to the `ScenarioStateContext` it is possible to use [Read from Response and set it to a Feature context](#read-from-response-and-set-it-to-a-feature-context).
But like mentioned at this point, this is an [Anti-Pattern](https://cucumber.io/docs/guides/anti-patterns/), which should be used with caution.

**Requires the `Steps` [Set a URI path for later execution](#set-a-uri-path-for-later-execution) and [Set a body from JSON file for later execution](#set-a-body-from-json-file-for-later-execution)!**
The used token depends on [Define that a token without scopes should be used](#define-that-a-token-without-scopes-should-be-used) `Step`.

##### Execute a PUT request call to previously given URL and body with dynamic URI elements
```gherkin
Scenario:
  When executing a PUT call with previously given API path, body and these dynamic 'URI Elements' replaced with the 'URI Values'
    | URI Elements  | URI Values |
    | resourceId    | abc-def-gh |
    | subResourceId | abc-def-gh |
```

Calls a previously given URL path and Body as a `PUT` request and replace dynamic URI elements with values.

In the example above the given link looks like: `/api/v1/endpoint/{resourceId}/{subResourceId}`.
The dynamic elements `{resourceId}` and `{subResourceId}` will be replaced with the values from the datatable below the sentence.

This datatable requires the header `| URI Elements  | URI Values |`.

The values do first a lookup in the `ScenarioStateContext`, if there is a key equal to the `URI Values` value.
If it finds the key, this key will be used, else it uses the value of the table directly.

To set something to the `ScenarioStateContext` it is possible to use [Read from Response and set it to a Feature context](#read-from-response-and-set-it-to-a-feature-context).
But like mentioned at this point, this is an [Anti-Pattern](https://cucumber.io/docs/guides/anti-patterns/), which should be used with caution.

**Requires the `Steps` [Set a URI path for later execution](#set-a-uri-path-for-later-execution) and [Set a body from JSON file for later execution](#set-a-body-from-json-file-for-later-execution)!**


#### PATCH requests
##### Execute a PATCH request to an endpoint with previously given URI and body
```gherkin
Scenario:
  When executing a PATCH call with previously given URI and body
```

Calls a previously given URI path as a `PATCH` request without `Authorization` header, and a previously given body.

##### Execute an authorized PATCH request call to an endpoint with previously given URI and body
```gherkin
Scenario:
  When executing an authorized PATCH call with previously given URI and body
```

Calls a previously given URL path as a `PATCH` request with `Authorization` header, and a previously given body.

##### Execute a PATCH request call to a URL with a previously given body
```gherkin
Scenario:
  When executing a PATCH call to {string} with previously given body
```

Calls the given URL path with a previously given Body as a `PATCH` request.

##### Execute an authorized PATCH request call to a URL with a previously given body
```gherkin
Scenario:
  When executing an authorized PATCH call to {string} with previously given body
```

Calls the given URL path with a previously given Body as a `PATCH` request.

The used token depends on [Define that a token without scopes should be used](#define-that-a-token-without-scopes-should-be-used) `Step`.


##### Execute a PATCH request call to an endpoint with body from file
```gherkin
Scenario:
  When executing a PATCH call to {string} with the body from file {string}
```

Calls the given URL path as a `PATCH` request without `Authorization` header, and a body defined in the given file.

##### Execute an authorized PATCH request call to an endpoint with body from file
```gherkin
Scenario:
  When executing an authorized PATCH call to {string} with the body from file {string}
```

Calls the given URL path as a `PATCH` request with `Authorization` header, and a body defined in the given file.
The used token depends on [Define that a token without scopes should be used](#define-that-a-token-without-scopes-should-be-used) `Step`.

##### Execute an authorized PATCH request call to previously given URL and body with dynamic URI elements
```gherkin
Scenario:
  When executing an authorized PATCH call with previously given API path, body and these dynamic 'URI Elements' replaced with the 'URI Values'
    | URI Elements  | URI Values |
    | resourceId    | abc-def-gh |
    | subResourceId | abc-def-gh |
```

Calls a previously given URL path and Body as a `PATCH` request and replace dynamic URI elements with values.

In the example above the given link looks like: `/api/v1/endpoint/{resourceId}/{subResourceId}`.
The dynamic elements `{resourceId}` and `{subResourceId}` will be replaced with the values from the datatable below the sentence.

This datatable requires the header `| URI Elements  | URI Values |`.

The values do first a lookup in the `ScenarioStateContext`, if there is a key equal to the `URI Values` value.
If it finds the key, this key will be used, else it uses the value of the table directly.

To set something to the `ScenarioStateContext` it is possible to use [Read from Response and set it to a Feature context](#read-from-response-and-set-it-to-a-feature-context).
But like mentioned at this point, this is an [Anti-Pattern](https://cucumber.io/docs/guides/anti-patterns/), which should be used with caution.

**Requires the `Steps` [Set a URI path for later execution](#set-a-uri-path-for-later-execution) and [Set a body from JSON file for later execution](#set-a-body-from-json-file-for-later-execution)!**
The used token depends on [Define that a token without scopes should be used](#define-that-a-token-without-scopes-should-be-used) `Step`.

##### Execute a PATCH request call to previously given URL and body with dynamic URI elements
```gherkin
Scenario:
  When executing a PATCH call with previously given API path, body and these dynamic 'URI Elements' replaced with the 'URI Values'
    | URI Elements  | URI Values |
    | resourceId    | abc-def-gh |
    | subResourceId | abc-def-gh |
```

Calls a previously given URL path and Body as a `PATCH` request and replace dynamic URI elements with values.

In the example above the given link looks like: `/api/v1/endpoint/{resourceId}/{subResourceId}`.
The dynamic elements `{resourceId}` and `{subResourceId}` will be replaced with the values from the datatable below the sentence.

This datatable requires the header `| URI Elements  | URI Values |`.

The values do first a lookup in the `ScenarioStateContext`, if there is a key equal to the `URI Values` value.
If it finds the key, this key will be used, else it uses the value of the table directly.

To set something to the `ScenarioStateContext` it is possible to use [Read from Response and set it to a Feature context](#read-from-response-and-set-it-to-a-feature-context).
But like mentioned at this point, this is an [Anti-Pattern](https://cucumber.io/docs/guides/anti-patterns/), which should be used with caution.

**Requires the `Steps` [Set a URI path for later execution](#set-a-uri-path-for-later-execution) and [Set a body from JSON file for later execution](#set-a-body-from-json-file-for-later-execution)!**



#### DELETE requests
##### Execute a DELETE request to an endpoint with previously given URI and body
```gherkin
Scenario:
  When executing a DELETE call with previously given URI and body
```

Calls a previously given URI path as a `DELETE` request without `Authorization` header, and a previously given body.

##### Execute an authorized DELETE request call to an endpoint with previously given URI and body
```gherkin
Scenario:
  When executing an authorized DELETE call with previously given URI and body
```

Calls a previously given URL path as a `DELETE` request with `Authorization` header, and a previously given body.

##### Execute a DELETE request call to a URL with a previously given body
```gherkin
Scenario:
  When executing a DELETE call to {string} with previously given body
```

Calls the given URL path with a previously given Body as a `DELETE` request.

##### Execute an authorized DELETE request call to a URL with a previously given body
```gherkin
Scenario:
  When executing an authorized DELETE call to {string} with previously given body
```

Calls the given URL path with a previously given Body as a `DELETE` request.

The used token depends on [Define that a token without scopes should be used](#define-that-a-token-without-scopes-should-be-used) `Step`.


##### Execute a DELETE request call to an endpoint with body from file
```gherkin
Scenario:
  When executing a DELETE call to {string} with the body from file {string}
```

Calls the given URL path as a `DELETE` request without `Authorization` header, and a body defined in the given file.

##### Execute an authorized DELETE request call to an endpoint with body from file
```gherkin
Scenario:
  When executing an authorized DELETE call to {string} with the body from file {string}
```

Calls the given URL path as a `DELETE` request with `Authorization` header, and a body defined in the given file.
The used token depends on [Define that a token without scopes should be used](#define-that-a-token-without-scopes-should-be-used) `Step`.

##### Execute an authorized DELETE request call to previously given URL and body with dynamic URI elements
```gherkin
Scenario:
  When executing an authorized DELETE call with previously given API path, body and these dynamic 'URI Elements' replaced with the 'URI Values'
    | URI Elements  | URI Values |
    | resourceId    | abc-def-gh |
    | subResourceId | abc-def-gh |
```

Calls a previously given URL path and Body as a `DELETE` request and replace dynamic URI elements with values.

In the example above the given link looks like: `/api/v1/endpoint/{resourceId}/{subResourceId}`.
The dynamic elements `{resourceId}` and `{subResourceId}` will be replaced with the values from the datatable below the sentence.

This datatable requires the header `| URI Elements  | URI Values |`.

The values do first a lookup in the `ScenarioStateContext`, if there is a key equal to the `URI Values` value.
If it finds the key, this key will be used, else it uses the value of the table directly.

To set something to the `ScenarioStateContext` it is possible to use [Read from Response and set it to a Feature context](#read-from-response-and-set-it-to-a-feature-context).
But like mentioned at this point, this is an [Anti-Pattern](https://cucumber.io/docs/guides/anti-patterns/), which should be used with caution.

**Requires the `Steps` [Set a URI path for later execution](#set-a-uri-path-for-later-execution) and [Set a body from JSON file for later execution](#set-a-body-from-json-file-for-later-execution)!**
The used token depends on [Define that a token without scopes should be used](#define-that-a-token-without-scopes-should-be-used) `Step`.

##### Execute a DELETE request call to previously given URL and body with dynamic URI elements
```gherkin
Scenario:
  When executing a DELETE call with previously given API path, body and these dynamic 'URI Elements' replaced with the 'URI Values'
    | URI Elements  | URI Values |
    | resourceId    | abc-def-gh |
    | subResourceId | abc-def-gh |
```

Calls a previously given URL path and Body as a `DELETE` request and replace dynamic URI elements with values.

In the example above the given link looks like: `/api/v1/endpoint/{resourceId}/{subResourceId}`.
The dynamic elements `{resourceId}` and `{subResourceId}` will be replaced with the values from the datatable below the sentence.

This datatable requires the header `| URI Elements  | URI Values |`.

The values do first a lookup in the `ScenarioStateContext`, if there is a key equal to the `URI Values` value.
If it finds the key, this key will be used, else it uses the value of the table directly.

To set something to the `ScenarioStateContext` it is possible to use [Read from Response and set it to a Feature context](#read-from-response-and-set-it-to-a-feature-context).
But like mentioned at this point, this is an [Anti-Pattern](https://cucumber.io/docs/guides/anti-patterns/), which should be used with caution.

**Requires the `Steps` [Set a URI path for later execution](#set-a-uri-path-for-later-execution) and [Set a body from JSON file for later execution](#set-a-body-from-json-file-for-later-execution)!**


#### Body manipulation
```gherkin
Scenario:
  When I set the value of the previously given body property {string} to {string}
```

This can manipulate a previously given body by exchanging a JSON element with the given value.
**Requires the `Step` [Set a body from JSON file for later execution](#set-a-body-from-json-file-for-later-execution)!**


### Then
#### Validate HTTP response code
```gherkin
Scenario:
  Then I ensure that the status code of the response is {int}
```

Validates, that the response is the expected HTTP code (e.g. `200`).


#### Validate response body with JSON file
```gherkin
Scenario:
  Then I ensure that the body of the response is equal to the file {string}
```

Validates, that the body of the response is equal to the given file.
Like mentioned above, this file can contain [JSON Unit](https://github.com/lukas-krecan/JsonUnit) syntax for dynamic field validation.

#### Validate response body with given String
```gherkin
Scenario:
  Then I ensure that the body of the response is equal to
    """
    {
      "field": "value",
    }
    """
```

In this case, the JSON is written directly under the sentence and enclosed in three double quotation marks.
Here it is also possible to use [JSON Unit](https://github.com/lukas-krecan/JsonUnit) syntax to validate dynamic elements.

#### Read from Response and set it to a `Feature` context
```gherkin
Scenario:
  Then I store the string of the field {string} in the context {string} for later usage
```

**Attention: This is an [Anti-Pattern](https://cucumber.io/docs/guides/anti-patterns/)!**

This can be used to write the value of a JSON element of the response to a context that is available through the `Feature` or other `Scenarios`.

Use this with caution, because at the point where the element is reused, the `Scenario` is hard coupled to this `Step` which ultimately makes it not executable as single `Step`.
On the other hand, this can be useful to support cross-`Features` testing with dynamic values for end-to-end testing.

# Extension of JSON Unit Matcher

It is possible to extend the JSON matchers by creating a new matcher and extending the `org.hamcrest.BaseMatcher` class and implementing the `com.ragin.bdd.cucumber.matcher.BddCucumberJsonMatcher` interface.

After they are created, you have to add them to the `@ContextConfiguration` classes definition.
See [CreateContextHooks.java](src/test/java/com/ragin/bdd/cucumbertests/hooks/CreateContextHooks.java) for an example how the configuration should look like.

## Simple matcher
A simple matcher to validate the current object as it is, can look like this:

```java
import com.ragin.bdd.cucumber.matcher.BddCucumberJsonMatcher;
import org.apache.commons.lang3.StringUtils;
import org.hamcrest.BaseMatcher;
import org.hamcrest.Description;
import org.springframework.stereotype.Component;

@Component
public class DividableByTwoMatcher extends BaseMatcher<Object> implements BddCucumberJsonMatcher {
    public boolean matches(Object item) {
        if (StringUtils.isNumeric(String.valueOf(item))) {
            // never do that, but it should show something ;)
            return Integer.parseInt((String) item) % 2 == 0;
        }
        return false;
    }

    @Override
    public void describeTo(Description description) {
        // nothing to describe here
    }

    @Override
    public String matcherName() {
        return "isDividableByTwo";
    }

    @Override
    public Class<? extends BaseMatcher<?>> matcherClass() {
        return this.getClass();
    }
}
```

Now you can use this matcher with the following statement in your expected JSON:

```json
{
  "number": "${json-unit.matches:isDividableByTwo}"
}
```

The `matcherName()` result is now part of the `json-unit.matches:` definition.

## Matcher with parameter

If you need parameter, you can implement also the `net.javacrumbs.jsonunit.core.ParametrizedMatcher` interface.
If there are several arguments, you can pass the arguments as JSON to the matcher and parse it here.
 
```java
import com.ragin.bdd.cucumber.matcher.BddCucumberJsonMatcher;
import net.javacrumbs.jsonunit.core.ParametrizedMatcher;
import org.apache.commons.lang3.StringUtils;
import org.hamcrest.BaseMatcher;
import org.hamcrest.Description;
import org.springframework.stereotype.Component;

@Component
public class DividableByNumberMatcher extends BaseMatcher<Object> implements ParametrizedMatcher, BddCucumberJsonMatcher {
    private String parameter;

    public boolean matches(Object item) {
        if (StringUtils.isNumeric(String.valueOf(item))) {
            // never do that, but it should show something ;)
            return Integer.parseInt((String) item) % Integer.parseInt(parameter) == 0;
        }
        return false;
    }

    @Override
    public void describeTo(Description description) {
        // nothing to describe here
    }

    @Override
    public String matcherName() {
        return "isDividableByNumber";
    }

    @Override
    public Class<? extends BaseMatcher<?>> matcherClass() {
        return this.getClass();
    }

    @Override
    public void setParameter(String parameter) {
        this.parameter = parameter;
    }
}
```

To pass the parameter to the matcher, the JSON has to look like this:


```json
{
  "number": "${json-unit.matches:isDividableByNumber}5"
}
```

If you want to pass a JSON, you have to do it with single quotes:


```json
{
  "number": "${json-unit.matches:isDividableByNumber}'{"myarg1": "A"}'"
}
```

