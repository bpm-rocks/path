BPM Library: Path
=================

Find your way around directory trees.


Installation
============

Add to your `bpm.ini` file the following dependency.

    [dependencies]
    0=path

Run `bpm install` to add the library. Finally, use it in your scripts.

    #!/usr/bin/env bash
    . bpm
    bpm::include path


API
===


[//]: # (AUTOGENERATED FROM libpath - START)

`path::absoluteDir()`
---------------------

Resolves a directory. If you are given a relative path, this turns it into an absolute path.

* $1 - Destination variable name.
* $2 - Path to resolve.
* $3 - Path to resolve against (defaults to current directory).

Returns true (0) when everything works. Returns false (1) when the directory does not exist (thus it can't be resolved). Returns false (2) when the path to resolve against does not exist.


`path::dirname()`
-----------------

Equivalent to calling `dirname` but does not make a subshell, so this is roughly twice as fast.

* $1 - Destination variable name. This is set to the parent folder.
* $2 - Filename or directory name.

Examples

    path::dirname dest a/file/somewhere
    echo "$dest"   # "a/file"

    path::dirname dest ./filename
    echo "$dest"   # "."

    path::dirname dest filename
    echo "$dest"   # "."

    path::dirname dest some/dir/
    echo "$dest"   # "some"

    path::dirname dest dir/
    echo "$dest"   # "."

Returns nothing.


`path::findParentContaining()`
------------------------------

Performs a single test for a target in the current directory or any parent. When found, supplies the folder name to the destination variable name. The location will be root-relative.

* $1 - Destination variable name.
* $2 - The type of test to perform.
* $3 - The target that you are testing.

Examples:

    # Search for a bpm.ini file in the current folder or any parent.
    if ! path::findParentContaining result -f bpm.ini; then
        echo "Sorry, did not find the file" >&2
    else
        echo "Folder containing file: $result"
        echo "Full path: $result/bpm.ini"
    fi

    # Search for a particular library
    path::findParentContaining -d bpm_modules/is

Returning success and an empty string is a valid response, so make sure you use the return code from the function.

Returns true (0) if the target was found.

[//]: # (AUTOGENERATED FROM libpath - END)


License
=======

This project is placed under an [MIT License](LICENSE.md).
