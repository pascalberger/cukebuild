# CUKE Build

CUKE is a free and open source cross-platform build automation system with a Gherkin DSL for tasks such as compiling code, copying files and folders, running unit tests, compressing files and building NuGet packages. CUKE scripts is readable by everyone within the organization, making it easier for business owners to participate in the build automation process.

## Getting started

Create a tool manifest available in your repository or create one using the following command:

```dotnetcli
dotnet new tool-manifest
```

Install CUKE as a local tool using the dotnet tool command:

```dotnetcli
dotnet tool install CUKE.Tool
```

## Example script

```gherkin
Feature: Build the App

  # Clean
  Scenario: Clean
    Given artifacts directory exists
    When the build is started
    Then the artifacts directory is cleaned

  # Restore
  Scenario: Restore
    Given the project contains package references
    And clean has been executed
    When the build is started
    Then NuGet packages are restored

  # Build
  Scenario: Build
    Given restore has been executed
    When the build is started
    Then the project is built using MSBuild

  # Test
  Scenario: Test
    Given build has been executed
    When the build is started
    Then the project is tested using XUnit

  # Package
  Scenario: Package
    Given test has been executed
    And all tests pass
    When the build is started
    Then the project is packaged as NuGet packages

  # Push
  Scenario: Push
    Given NuGet packages exist
    And branch is main
    When the build is started
    Then the packages are pushed to nuget.org
```

Run the script.

```dotnetcli
dotnet cuke build build.cuke
```

## Acknowledgements

Cucumber photo by [Markus Winkler](https://unsplash.com/@markuswinkler?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/cucumber?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText).
