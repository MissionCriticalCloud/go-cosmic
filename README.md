go-cosmic
=============
A Cosmic API client enabling Go programs to interact with Cosmic in a simple and uniform way

## Status

This package covers the complete Cosmic API and is well tested. Of course there will still be untested corner cases when you have over 400 API commands that you can use, but over all it's save to use this package.

To be able to find the API command you want, they are grouped by 'services' which match the grouping you can see/find on the [Cosmic API docs](http://apidoc.cosmiccloud.io/) website.

## Usage

The cosmic package is always generated against the latest stable Cosmic release (currently v5.3.x). Luckily the API doesn't change that much, and were it does we try to make sure the generated package is able handle both the old and the new case. Over time it will be impossible to support all version with just one package, but until now we seem to manage this pretty well.

To generate a new version yourself, you must update `api.go` in the `go-cosmic/generate` directory. This file contains the output from the apidocs website (use the regex.txt) and the `listApis` call (use cloudmonkey with json output).

Additionaly you need the following Go package installed:
`go get golang.org/x/tools/cmd/goimports`

Then go into the `go-cosmic/generate` directory and just build and run:
`go build`
`./generate`

Please see the package documentation on [GoDocs](http://godoc.org/github.com/xanzy/go-cosmic/cosmic).

## Features

Next to the API commands Cosmic itself offers, there are a few additional features/function that are helpful. For starters there are two clients, an normal one (created with `NewClient(...)`) and an async client (created with `NewAsyncClient(...)`). The async client has a buildin waiting/polling feature that waits for a configured amount of time (defaults to 300 seconds) on running async jobs. This is very helpfull if you do not want to continue with your program execution until the async job is done.

There is also a function you can call manually (`GetAsyncJobResult(...)`) that does the same, but then as a seperate call after you started the async job.

Another nice feature is the fact that for every API command you can create the needed parameter struct using a `New...Params` function, like for example `NewListTemplatesParams`. The advantage of using this functions to create a new parameter struct, is that these functions know what the required parameters are of ever API command, and they require you to supply these when creating the new struct. Every additional paramater can be set after creating the struct by using `SetName()` like functions.

Last but not least there are a whole lot of helper function that will try to automatically find an UUID for you for a certain item (disk, template, virtualmachine, network...). This makes it much easier and faster to work with the API commands and in most cases you can just use then if you know the name instead of the UUID.

## ToDO

I fully understand I need to document this all a little more/better and there should also be some tests added.

## Getting Help

_Please try to see if [GoDocs](http://godoc.org/github.com/xanzy/go-cosmic) can provide some answers first!_

* If you have an issue: report it on the [issue tracker](https://github.com/xanzy/go-cosmic/issues)

## Author

Sander van Harmelen (<sander@xanzy.io>)

## License

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at <http://www.apache.org/licenses/LICENSE-2.0>
