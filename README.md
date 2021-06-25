<h1 align="center">
    <a href="https://github.com/WolfSoftware">
        <img src="https://raw.githubusercontent.com/WolfSoftware/branding/master/images/general/banners/64/black-and-white.png" alt="Wolf Software Logo" />
    </a>
    <br />
    JSON Lint for CI/CD Pipelines
</h1>

<p align="center">
    <a href="https://github.com/CICDToolbox/json-lint/actions/workflows/pipeline.yml">
        <img src="https://img.shields.io/github/workflow/status/CICDToolbox/json-lint/pipeline/master?logo=github&logoColor=white&style=for-the-badge" alt="Github Build Status">
    </a>
    <a href="https://travis-ci.com/CICDToolbox/json-lint">
        <img src="https://img.shields.io/travis/com/CICDToolbox/json-lint/master?style=for-the-badge&logo=travis" alt="Travis Build Status">
    </a>
    <a href="https://github.com/CICDToolbox/json-lint/releases/latest">
        <img src="https://img.shields.io/github/v/release/CICDToolbox/json-lint?color=blue&style=for-the-badge&logo=github&logoColor=white&label=Latest%20Release" alt="Release">
    </a>
    <a href="https://github.com/CICDToolbox/json-lint/releases/latest">
        <img src="https://img.shields.io/github/commits-since/CICDToolbox/json-lint/latest.svg?color=blue&style=for-the-badge&logo=github&logoColor=white" alt="Commits since release">
    </a>
    <br />
    <a href=".github/CODE_OF_CONDUCT.md">
        <img src="https://img.shields.io/badge/Code%20of%20Conduct-blue?style=for-the-badge&logo=read-the-docs&logoColor=white" />
    </a>
    <a href=".github/CONTRIBUTING.md">
        <img src="https://img.shields.io/badge/Contributing-blue?style=for-the-badge&logo=read-the-docs&logoColor=white" />
    </a>
    <a href=".github/SECURITY.md">
        <img src="https://img.shields.io/badge/Report%20Security%20Concern-blue?style=for-the-badge&logo=read-the-docs&logoColor=white" />
    </a>
    <a href="https://github.com/CICDToolbox/json-lint/issues">
        <img src="https://img.shields.io/badge/Get%20Support-blue?style=for-the-badge&logo=read-the-docs&logoColor=white" />
    </a>
    <br />
    <a href="https://github.com/TGWolf">
        <img src="https://img.shields.io/badge/Created%20by%20Wolf-black?style=for-the-badge" />
    </a>
</p>

## Overview

A tool to check your JSON files in travis-ci pipelines using [jq](https://stedolan.github.io/jq/).

> Also see: [validate-json](https://github.com/DevelopersToolbox/validate-json) for our bash plugin to do the same thing.

This tool has been written and tested using both GitHub Actions and Travis CI, but it should work out of the box with a lot of other CI/CD tools.

## Usage

### GitHub Actions


```yml
on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    - name: Set up Ruby 3.0
      uses: ruby/setup-ruby@v1
      with:
        ruby-version: 3.0	
    - name: Run JSON Lint
      run: wget --quiet -O - https://raw.githubusercontent.com/CICDToolbox/json-lint/master/pipeline.sh | bash
```

### Travis CI

```yml
language: ruby
rvm: 3.0

script:
  - wget --quiet -O - https://raw.githubusercontent.com/CICDToolbox/json-lint/master/pipeline.sh | bash
```

### Other Options

The following environment variables can be set in order to customise the script.

| Name          | Purpose |
| ------------- | ------- |
| REPORT_ONLY   | Generate the report but do not fail the build even if an error occurred. |
| SHOW_ERRORS   | Show the actual errors instead of just which files had errors. |

You can use any combination of the above settings.

#### GitHub Actions

```yml
on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    - name: Run JSON Lint
      env:
        REPORT_ONLY: true
        SHOW_ERRORS: true
      run: wget --quiet -O - https://raw.githubusercontent.com/CICDToolbox/json-lint/master/pipeline.sh | bash
```

#### Travis CI

```yml
language: ruby
rvm: 3.0

env:
  - REPORT_ONLY=true
  - SHOW_ERRORS=true

script:
  - wget --quiet -O - https://raw.githubusercontent.com/CICDToolbox/json-lint/master/pipeline.sh | bash
```

## Example Output

This is an example of the output report generated by this tool, this is the actual output from the tool running against itself.

```
--------------------------------------------------------------------------------
                    Scanning all JSON with jq (version: 1.6)
--------------------------------------------------------------------------------
 [  OK  ] Processing successful for tests/data.json
--------------------------------------------------------------------------------
                     Total: 1, OK: 1, Failed: 0, Skipped: 0
--------------------------------------------------------------------------------
```

## File Identification

Target files are identified using the following code:

```shell
file -b "${filename}" | grep -qE '^JSON'

AND

[[ ${filename} =~ \.json$ ]]
```

## Show Support

<p>
	<a href="https://ko-fi.com/wolfsoftware">
		<img src="https://img.shields.io/badge/Ko%20Fi-blue?style=for-the-badge&logo=ko-fi&logoColor=white" />
	</a>
</p>
