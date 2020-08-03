[![npm version](https://img.shields.io/npm/v/bunyan.svg?style=flat)](https://www.npmjs.com/package/bunyan)
[![Build Status](https://travis-ci.org/trentm/node-bunyan.svg?branch=master)](https://travis-ci.org/trentm/node-bunyan)

### bunyan-adanic
**The only diffrence between this package and node-bunyan
is that when logging that when pipe logs to bunyan that library show time like this**
`[2020-08-03T05:33:48.703Z] DEBUG:`

**but when using this package show you like this:**

`[2020-08-03-10:03:48.703] DEBUG:`

## All of changes have been made in this package from bunyan
* Rename `bin/adanic` to `bin/bunyan-adanic`
* Change `"bin": { "bunyan": "./bin/bunyan"}`
            to
            `            "bin": { "bunyan-adanic": "./bin/bunyan-adanic" }`
* Add this line to [bin/bunyan/adanic](https://github.com/mohammadranjbar/node-bunyan/tree/master/bin/bunyan-adanic)
`time = "["+moment(rec.time,'[[]YYYY-MM-DD[T]HH:mm:ss.SSSZ[]]').
           format(process.env.TIME_FORMAT || 'YYYY-MM-DD/HH:mm:ss.SSS')+"]"
`

### CLI Usage
`npm i -g bunyan-adnaic`
Bunyan log output is a stream of JSON objects. This is great for processing, but not for reading directly. A bunyan tool is provided for pretty-printing bunyan logs and for filtering (e.g. | bunyan -c 'this.foo == "bar"'). Using our example above:

`$ node hi.js | bunyan-adanic`

    [2013-01-04T19:01:18.241]  INFO: myapp/40208 on banana.local: hi
    [2013-01-04T19:01:18.242]  WARN: myapp/40208 on banana.local: au revoir (lang=fr)
See the screenshot above for an example of the default coloring of rendered log output. That example also shows the nice formatting automatically done for some well-known log record fields (e.g. req is formatted like an HTTP request, res like an HTTP response, err like an error stack trace).

One interesting feature is filtering of log content, which can be useful for digging through large log files or for analysis. We can filter only records above a certain level:

`$ node hi.js | bunyan-adanic -l warn`

    [2013-01-04T19:08:37.182]  WARN: myapp/40353 on banana.local: au revoir (lang=fr)

Or filter on the JSON fields in the records (e.g. only showing the French records in our contrived example):
