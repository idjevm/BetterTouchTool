# BetterTouchTool

This contains the BetterTouchTool documentation and issue tracking for [BetterTouchTool](https://boastr.net).

* Please post any bugs, feature requests, ideas or even questions (with the appropriate tags) in the [issues section](https://github.com/fifafu/BetterTouchTool/issues?q=is%3Aissue+is%3Aopen+sort%3Aupdated-desc).
* Some issues are marked as FAQ/Knowledge base, which may be interesting for everybody. View them [here](https://github.com/fifafu/BetterTouchTool/issues?q=is%3Aissue+label%3A%22%E2%9C%B3%EF%B8%8F+Knowledge+Base+%2F+FAQ%22).
* The current BetterTouchTool release notes can always be found [here](https://updates.bettertouchtool.net/bettertouchtool_release_notes.html).

For non-public issues, please contact me via boastr.net@gmail.com.

## BetterTouchTool Documentation

The BetterTouchTool documentation can be found [here](http://docs.bettertouchtool.com/). Pull requests on the BetterTouchTool documentation (which is hosted on this repo) are always very welcome.

To build the BetterTouchTool Documentation follow these steps:

* Install Node.js (I recommend to use [nvm](https://github.com/creationix/nvm) to install Node. Current long term support version of Node.js is v6.9.1).
* Run ``npm install -g gitbook-cli``
* cd into the BetterTouchToolDocs directory and run ``node yarn-0.17.10.js install``
* run ``gitbook serve`` to build and run the documentation
* run ``gitbook build`` to just build the documentation
