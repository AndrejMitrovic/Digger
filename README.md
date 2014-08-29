# Digger

Digger is a tool for working with D's source code and its history.
It can build D (including older D versions), customize the build with pending pull requests or forks,
and find the exact pull request which introduced a regression (or fixed a bug).

### Requirements

Git is required.

Currently, you must have Microsoft Visual Studio 2010 and Windows SDK v7.0A installed to build for Windows/64.

### Building

    $ git clone --recursive https://github.com/CyberShadow/Digger
    $ cd Digger
    $ rdmd --build-only digger
    $ rdmd --build-only digger-web

On Windows, you may see:

    Warning 2: File Not Found version.lib

This is a benign warning.

### Web interface

Run digger-web to start the web interface, which allows interactively customizing a D version to build.

### Configuration

You can optionally configure a few settings using a configuration file.
To do so, copy `digger.ini.sample` to `digger.ini` and adjust as instructed by the comments.

### Command-line usage

##### Building D

    # build latest master branch commit
    $ digger build

    # build a specific D version
    $ digger build v2.064.2

    # build for x86-64
    $ digger build --64 v2.064.2

    # build commit from a point in time
    $ digger build "@ 3 weeks ago"

    # build latest 2.065 (release) branch commit
    $ digger build 2.065

    # build specified branch from a point in time
    $ digger build "2.065 @ 3 weeks ago"

    # build with added pull request
    $ digger build "master + dmd#123"

    # build with added GitHub fork branch
    $ digger build "master + Username/dmd/awesome-feature"

##### Bisecting

To bisect D's history to find which pull request introduced a bug, first copy `bisect.ini.sample` to `bisect.ini`, adjust as instructed by the comments, then run:

    $ digger bisect path/to/bisect.ini
