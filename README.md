# Some doom3 mods adapted for dhewm3

ok, just one currently...

## How to use this Repository/Compiling

This repository is supposed to be cloned to `/path/to/your-dhewm3/neo/mods/`
and currently needs my mod-support branch:
https://github.com/DanielGibson/dhewm3/tree/mod-support

Then just create your dhewm3 Makefiles with 
`cmake -DMODS=ON ../neo/`
and compile as usual. See the dhewm3 project for details.

## How it works

The actual mods lie in the [dhewm3-base-mods](https://github.com/DanielGibson/dhewm3-base-mods)
repository, one branch per mod (the master branch is just the vanilla base game code from dhewm3)
and are "linked" as git submodules.
