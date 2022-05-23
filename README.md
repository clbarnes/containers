# Useful apptainer images

## Adding recipes

Images should be deterministic: avoid any steps which fetch the "latest" version of anything (e.g. cloning from github without specifying a tag or commit, running unbounded updaters).
Write the version of the included tool(s) in a file called `/VERSION` in the container.
If you must run anything non-deterministic, at least store the datetime: `date +'%Y-%m-%dT%H:%M' > /VERSION`

Do not edit the `Makefile` manually.
Instead, run `./create_makefile.py > Makefile` to auto-discover and write recipes for all containers.

Don't forget to add the name of the recipe to `./.github/workflows/ci.yaml:jobs.build.strategy.matrix.container`.

## Checking package versions

Read the `/VERSION` file with

    apptainer exec path/to/image.sif cat /VERSION

Exactly what this means will depend on the container.
