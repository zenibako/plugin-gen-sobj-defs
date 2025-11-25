# sf-plugin-gen-sobj-defs

[![NPM](https://img.shields.io/npm/v/sf-plugin-gen-sobj-defs.svg?label=sf-plugin-gen-sobj-defs)](https://www.npmjs.com/package/sf-plugin-gen-sobj-defs) [![Downloads/week](https://img.shields.io/npm/dw/sf-plugin-gen-sobj-defs.svg)](https://npmjs.org/package/sf-plugin-gen-sobj-defs) [![License](https://img.shields.io/badge/License-Apache--2.0-blue.svg)](https://opensource.org/license/apache-2-0)

A Salesforce CLI plugin that generates or refreshes local SObject definitions (faux Apex classes) for code completion in your IDE.

## About

This plugin connects to your Salesforce org, fetches SObject metadata, and generates Apex class representations that include all fields with proper type mappings. These definitions provide IntelliSense and type checking when working with Salesforce objects in your code.

The generated files are placed in the `.sfdx/tools/sobjects/` directory of your Salesforce project, organized into `standardObjects/` and `customObjects/` subdirectories.

### Why This Plugin?

The "SFDX: Refresh SObject Definitions" command in the Salesforce VS Code extensions requires the full VS Code extension to be running. This plugin provides the same functionality as a standalone CLI command, making it useful for:

- **CI/CD pipelines** - Generate SObject definitions in automated builds
- **Non-VS Code editors** - Use with Neovim, Emacs, or other editors with Apex LSP support
- **Scripting** - Automate SObject definition refresh as part of project setup

## Install

```bash
sf plugins install sf-plugin-gen-sobj-defs
```

## Usage

```bash
# Refresh all SObject definitions
sf sobject refresh definitions --target-org myOrg

# Refresh only custom SObjects
sf sobject refresh definitions --target-org myOrg --sobject-category custom

# Refresh only standard SObjects
sf sobject refresh definitions --target-org myOrg --sobject-category standard
```

## Commands

<!-- commands -->

- [`sf sobject refresh definitions`](#sf-sobject-refresh-definitions)

## `sf sobject refresh definitions`

Refresh SObject definitions for your org.

```
USAGE
  $ sf sobject refresh definitions -o <value> [--json] [--flags-dir <value>] [--sobject-category all|custom|standard]
    [--api-version <value>]

FLAGS
  -o, --target-org=<value>           (required) Username or alias of the target org.
      --api-version=<value>          Override the API version used for the connection.
      --sobject-category=<option>    [default: all] The category of SObjects to refresh.
                                     <options: all|custom|standard>

GLOBAL FLAGS
  --flags-dir=<value>  Import flag values from a directory.
  --json               Format output as json.

DESCRIPTION
  Refresh SObject definitions for your org.

  Generates or refreshes local SObject definitions (faux classes) for code completion in your IDE. These definitions
  help with IntelliSense and type checking when working with Salesforce objects in your code.

  You can choose to refresh all SObjects, only custom objects, or only standard objects. The command connects to your
  target org and fetches the latest SObject metadata.

EXAMPLES
  Refresh all SObject definitions:

    $ sf sobject refresh definitions --target-org myOrg

  Refresh only custom SObject definitions:

    $ sf sobject refresh definitions --target-org myOrg --sobject-category custom

  Refresh only standard SObject definitions:

    $ sf sobject refresh definitions --target-org myOrg --sobject-category standard
```

_See code: [src/commands/sobject/refresh/definitions.ts](https://github.com/zenibako/plugin-gen-sobj-defs/blob/main/src/commands/sobject/refresh/definitions.ts)_

<!-- commandsstop -->

## Issues

Please report any issues at https://github.com/zenibako/plugin-gen-sobj-defs/issues

## Contributing

1. Please read our [Code of Conduct](CODE_OF_CONDUCT.md)
2. Create a new issue before starting your project so that we can keep track of what you are trying to add/fix.
3. Fork this repository.
4. [Build the plugin locally](#build)
5. Create a _topic_ branch in your fork.
6. Edit the code in your fork.
7. Write appropriate tests for your changes. Try to achieve at least 95% code coverage on any new code.
8. Send us a pull request when you are done.

### Build

To build the plugin locally, make sure to have yarn installed and run the following commands:

```bash
# Clone the repository
git clone git@github.com:zenibako/plugin-gen-sobj-defs.git

# Install the dependencies and compile
yarn && yarn build
```

To use your plugin, run using the local `./bin/dev.js` file:

```bash
./bin/dev.js sobject refresh definitions --target-org myOrg
```

To link the plugin to Salesforce CLI for testing:

```bash
sf plugins link .
sf plugins  # verify the plugin is linked
```

## Attribution

This plugin is based on the SObject refresh functionality from the [Salesforce VS Code Extensions](https://github.com/forcedotcom/salesforcedx-vscode). The core logic is derived from [`refreshSObjects.ts`](https://github.com/forcedotcom/salesforcedx-vscode/blob/develop/packages/salesforcedx-vscode-core/src/commands/refreshSObjects.ts) in the `salesforcedx-vscode-core` package.

## License

Apache-2.0
