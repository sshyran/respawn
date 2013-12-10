# respawn

Spawn a process and restart it if it crashes.

	npm install respawn

## Usage

It is easy to use

``` js
var respawn = require('respawn');

var monitor = respawn(['node', 'server.js'], {
	env: {ENV_VAR:'test'}, // set env vars
	cwd: '.',              // set cwd
	maxRestarts:10,        // how many restarts are allowed within 60s
	sleep:1000,            // time to sleep between restarts
});

monitor.start(); // spawn and watch
```

Optionally you can specify the command to to spawn in the option map as `command: [...]`

## API

* `monitor.start()` Starts the monitor

* `monitor.stop()` Stops the monitor (kills the process if its running with SIGTERM)

* `monitor.status` Get the current monitor status. Available values are `running`, `stopping`, `stopped` and `sleeping`

## Events

* `monitor.on('start')` The monitor has started

* `monitor.on('stop')`  The monitor has fully stopped and the process is killed

* `monitor.on('sleep')` monitor is sleeping

* `monitor.on('spawn', process)` New child process has been spawned

* `monitor.on('exit', code, signal)` child process has exited

* `monitor.on('stdout', data)` child process stdout has emitted data

* `monitor.on('stderr', data)` child process stderr has emitted data

* `monitor.on('warn', err)` child process has emitted an error

## License

MIT