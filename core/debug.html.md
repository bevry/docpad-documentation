```
title: "Debugging"
```

Sometimes things go bad, and you need to get into DocPad and work out what’s happening. A plugin may be not working as expected, content isn’t being generated, or you may just curious as to how to do it. 

Well, for that you’ll need to get your debugging on.


## What you’ll need

1. Get a Webkit based browser (both [Google Chrome](http://www.google.com/chrome/) and Safari work great)


## Debugging with [Node Inspector](https://github.com/dannycoates/node-inspector)

1. Install Node Inspector with the following:

	``` bash
	npm install -g node-inspector
	```

1. Open Node Inspector up by running `node-inspector` in another Terminal window:

1. Open up our local DocPad instance for debugging by running:

	``` bash
	docpad-debug run
	```

1. Navigate to http://127.0.0.1:8080/debug?port=5858 in your webkit based browser and start debugging (sometimes you may have to refresh or restart the Node inspector or DocPad instances).


## Debugging with [TraceGL](https://trace.gl/) - shareware

1. [Get TraceGL from their website](https://trace.gl/)

2. Download it to somewhere in your `PATH`, and run the following on it:

	``` bash
    mv tracegl.js tracegl
    chmod +x tracegl
    ```

3. Run TraceGL on DocPad

	``` bash
    docpad-trace run
    ```

4. Follow the outputted instructions


## Profiling with [NodeTime](https://nodetime.com/)

1. [Get a NodeTime account](https://nodetime.com/)

2. Add your NodeTime API KEY to your environment (we recommend the following):

	``` bash
	export NODETIME_KEY='YOUR_KEY'
	printf "\n\n# NodeTime API Key\nexport NODETIME_KEY='YOUR_KEY'" >> ~/.bash_profile
	```

3. Run DocPad with the `--profile` flag, so:

	``` bash
    docpad --profile run
    ```

4. Follow the instructions that output


## Profiling with [Node Webkit Agent](https://github.com/c4milo/node-webkit-agent)

1. Run DocPad with the `--profile` flag, so:

	``` bash
    docpad --profile run
    ```

2. Run `kill -SIGUSR2 123` (with `123` being the output process id, or PID)

3. [Open the Node Webkit Agent interface](http://c4milo.github.io/node-webkit-agent/26.0.1410.65/inspector.html?host=localhost:9999&page=0)
