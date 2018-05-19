# NOTE: BetterTouchTool is no longer using GitHub for Issue Tracking.
All bugs, feature requests or questions should be posted on the new community platform https://community.folivora.ai from now on. Existing issues will be moved in the coming days and weeks. For more information see https://folivora.ai/blog

<a href="https://community.folivora.ai">
<img src="community_moved.png"/>
  </a>

## BetterTouchTool Documentation

The BetterTouchTool documentation can be found [here](http://docs.bettertouchtool.com/). Pull requests on the BetterTouchTool documentation (which is hosted on this repo) are always very welcome.

To build the BetterTouchTool Documentation follow these steps:

* Install Node.js (I recommend to use [nvm](https://github.com/creationix/nvm) to install Node. Current long term support version of Node.js is v6.9.1).
* Run ``npm install -g gitbook-cli``
* cd into the BetterTouchToolDocs directory and run ``node yarn-0.17.10.js install``
* run ``gitbook serve`` to build and run the documentation
* run ``gitbook build`` to just build the documentation
