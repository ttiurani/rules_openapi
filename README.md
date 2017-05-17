# bazel open rules [![Build Status](https://travis-ci.org/meetup/rules_openapi.svg?branch=master)](https://travis-ci.org/meetup/rules_openapi)

> [Bazel](https://bazel.build/) rules for generating sources and libraries from [openapi](https://www.openapis.org/) schemas

## Rules

* [openapi_gen](#openapi_gen)

## Getting started

To use the Openapi rules, add the following to your projects `WORKSPACE` file

```python
rules_openapi_version="xxx" # update this as needed

git_repository(
    name = "io_bazel_rules_openapi",
    commit = rules_openapi_version,
    remote = "git@github.com:meetup/rules_openapi.git",
)

load("@io_bazel_rules_openapi//openapi:openapi.bzl", "openapi_repositories")
openapi_repositories()
```

Then in your `BUILD` file, just add the following so the rules will be available:

```python
load("@io_bazel_rules_openapi//openapi:openapi.bzl", "openapi_gen")
```

## openapi_gen

```python
open_api(name, spec, api_package, model_package, invoker_package)
```

Generates `.srcjar` containing generated source files from a given openapi specification

These rules rely on [swagger-codegen](https://github.com/swagger-api/swagger-codegen#swagger-code-generator) which defines many [configuration options](https://github.com/swagger-api/swagger-codegen#to-generate-a-sample-client-library). Not all configuration options
are implemented in these rules yet but contributions are welcome. You can also request features [here](https://github.com/meetup/rules_openapi/issues/new?title=I%20would%20like%20to%20see...)

<table class="table table-condensed table-bordered table-params">
  <colgroup>
    <col class="col-param" />
    <col class="param-description" />
  </colgroup>
  <thead>
    <tr>
      <th colspan="2">Attributes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>name</code></td>
      <td>
        <code>Name, required</code>
        <p>A unique name for this rule.</p>
      </td>
    </tr>
    <tr>
      <td><code>spec</code></td>
      <td>
        <code>String, required</code>
        <p>
          Path to <code>.yaml</code> or <code>.json</code> file containing openapi specification
        </p>
      </td>
    </tr>
    <tr>
      <td><code>language</code></td>
      <td>
        <code>String, required</code>
        <p>Name of language to generate. If you wish to use a custom language, you'll need to create a jar containing your <a href="https://github.com/swagger-api/swagger-codegen#making-your-own-codegen-modules">custom codegen module</a> use <code>deps</code> add the custom codegen module to the classpath.</p>
        <p>
          Note, not all swagger codegen provided langugages generate the exact same source given the exact same set of arguments.
          Be aware of this in cases where you expect bazel not to perform a previous executed action for the same sources.
        </p>
      </td>
    </tr>
    <tr>
      <td><code>api_package</code></td>
      <td>
        <code>String, optional</code>
        <p>package for api.</p>
      </td>
    </tr>
    <tr>
      <td><code>module_package</code></td>
      <td>
        <code>String, optional</code>
        <p>package for models.</p>
      </td>
    </tr>
    <tr>
      <td><code>invoker_package</code></td>
      <td>
        <code>String, optional</code>
        <p>package for invoker.</p>
      </td>
    </tr>
  </tbody>
</table>

Meetup 2017
