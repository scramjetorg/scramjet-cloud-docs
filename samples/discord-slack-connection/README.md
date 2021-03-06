# Discord to Slack (and vice versa) Connection

___

### The video that illustrates the execution of the sample is on our [YouTube](https://www.youtube.com/channel/UChgTmKeuAsKj8kDnylkmP6Q) channel [How to Connect Discord and Slack in 4 minutes](https://www.youtube.com/watch?v=y2L1f-f-wLM&t=1s).

___

> 💡 **Please note that the sample below requires some previous installations before you start running it, you will find them [here](../../README.md#3-install-scramjet-transform-hub).**

In this project you will find 4 STH Sequences:

* [discord-read](./discord-read/)
* [discord-write](./discord-write/)
* [slack-read](./slack-read/)
* [slack-write](./slack-write/)

You must run at least two (discord-read, slack write or discord-write, slack-read) in order to get one directional communication or all four for bi-directional communication.

Each Sequence either reads or writes to specified application respectively and uses `const TOPIC = ...` topic to exchange data between applications. You need two topics for bi-directional communication.

## TODO

As there is no way to map message IDs between the two applications, threads are not supported.

In order to get this working, Sequences must keep a track of posted and written IDs.

## Known Issues

<!-- TODO - check if this issues still apply -->

STH `v0.13` if installed via `npm` has an issue with `objectMode: true`. You will get an error like:

```bash
TypeError [ERR_INVALID_ARG_TYPE]: The "chunk" argument must be of type string or an Instance of Buffer or Uint8Array. 
Received an Instance of Object
```

If that happens either use `v0.14` if available or rebuild and run STH from repo. Please check [transform-hub documentation](https://github.com/scramjetorg/transform-hub/#build-the-packages-building_construction) for details.

Moreover, in case of `discord-read` you may get some issues with `discord.js` package. As a workaround run STH with `--no-docker` parameter like so: `./dist/sth/bin/hub.js --no-docker`
