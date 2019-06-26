# moor

An opinionated set of tools to help build docker images.

## Installing

The moor cli is available via pypi. To install simply run:

    pip3 install moor

## A `moor.toml` file

The central idea behind moor is to try and make creating and naming docker images slightly easier.
It does this my using a toml configuration file at the root of the project. Below is an example of
the one of these files:

    $ cat moor.toml

    registry = "gcr.io/foo-bar-baz"
    name = "example"
    version = "0.1.5"

In general all the fields of the configuration file should be optional and that `moor` should try
and calculate sensible defaults. See the [Defaults](#defaults) section for more information.

## Building the image

This command will build the docker the docker image.

    $ moor build

By default this image will created with the full tag name: [registry]/[name]:[version]

## Publising the image

The following command will build the latest version of the image and pushes the image to the
configured registry.

    $ moor pubish

## Getting information

To see what the current information for the project simply run the following command:

    $ moor info

This will display an output similar to the following

          Name: example
    Latest Tag: example:latest
     Local Tag: example:0.1.5
    Remove Tag: gcr.io/foo-bar-baz/example:0.1.5

## Reference

For a full reference of the all the options use the following command:

    $ moor --help

Here is an example output

    usage: moor [-h] [--debug] [-v] {build,info,publish,remove-old} ...

    positional arguments:
      {build,info,publish,remove-old}
        build               Builds a docker image
        info                Prints useful information about a build
        publish             Builds and pushes the image to the remove repository
        remove-old          Removes old containers and images for the context

    optional arguments:
      -h, --help            show this help message and exit
      --debug               Enable extra debugging
      -v, --version         Print the version and exit

## Defaults

* If `name` is not present then the name of the parent directory will be used
* If `version` is not presnet then the version returned from `git describe --always -dirty-wip` will
  be used, if this fails it will revert to "lastest"

