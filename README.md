# NOTE: THIS IS DEPRECATED!

**I think I found a better way for mod support in dhewm3: by providing an SDK, similar to the original Mod SDK.  
See https://github.com/dhewm/dhewm3-sdk for details.  
It already contains Dentonmod and Classic Doom 3, and more will follow soon!**

I'll only keep this stuff here for reference.


# Some Doom3 mods adapted for dhewm3

Two mods already: [Denton's Enhanced Doom3](http://doom3.filefront.com/file/Dentons_Enhanced_Doom3;76838)
and [Classic Doom 3](http://www.moddb.com/mods/classic-doom-3)!

## How to use this Repository/Compiling

Currently this needs my mod-support branch:  
https://github.com/DanielGibson/dhewm3/tree/mod-support

Clone dhewm3, change to the mod-support branch and pull

	git clone https://github.com/DanielGibson/dhewm3.git
	cd dhewm3
	git checkout mod-support

Then this (dhewm3-mods) repository must be cloned to `/path/to/your-dhewm3/neo/mods/`

That's done like this:  

	cd /path/to/your-dhewm3/neo/
	git clone --recurse-submodules https://github.com/DanielGibson/dhewm3-mods.git mods

`--recurse-submodules` will make sure that the submodules (containing the mods) will
be cloned as well.

Then just create your dhewm3 Makefiles with something like:  

	cd /path/to/your-dhewm3/
	mkdir build-with-mods
	cd build-with-mods
	cmake -DMODS=ON ../neo/

and compile as usual.  
See the [dhewm3 README](https://github.com/dhewm/dhewm3/blob/master/README.md)
for details on compiling (dependencies etc).

### Getting mod game data

The mod directories contain a README.txt that will tell you where to get the 
mods data (levels etc) and possibly how to install it.

## How it works

The actual mods lie in the [dhewm3-base-mods](https://github.com/DanielGibson/dhewm3-base-mods)
repository, one branch per mod (the master branch is just the vanilla base game code from dhewm3)
and are "linked" as git submodules.

dhewm3's cmake (at least in the aforementioned branch) adds the CMakeLists.txt of this
repository and the CMakeLists.txt adds all the linked mod subdirectories (which
themselves have their own CMakeLists.txt).

## How to add other mods

https://github.com/DanielGibson/dhewm3-base-mods#readme has information how to add
additional mods.

Please note that the mods sourcecode must be available for that - and to be
included in this repository it must be under GPLv3 (that's the license 
**id Software** used to release the Doom3 Source) - and *not* just Doom3 SDK License.  
That's because mixing GPL code and SDK Licensed code is illegal.  
This means that the mod authors/coders need to agree to publish their source under GPLv3.

If you are a mod author and want your mod in this list (and thus making
it playable on all platforms supported by dhewm3 and possibly other 
Doom3 ports), but can't port it to dhewm3 yourself (or don't  have the 
time or whatever), get in touch, maybe I can help you :-)


Cheers,

-Daniel
