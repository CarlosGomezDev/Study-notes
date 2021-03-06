`2021-01-18, Node.js child_process, Cluster, Worker Thread`
<br>https://nodejs.org/api/

## child_process module

The `child_process` module provides the ability to spawn subprocesses.

Each of the methods returns a `ChildProcess` instance and implement the Node.js `EventEmitter` API, allowing the parent process to register listener functions that are called when certain events occur during the life cycle of the child process. The `child_process.exec()` and `child_process.execFile()` methods additionally allow for an optional callback function to be specified that is invoked when the child process terminates.

By default, pipes for `stdin`, `stdout`, and `stderr` are established between the parent Node.js process and the spawned subprocess. These pipes have limited (and platform-specific) capacity. If the subprocess writes to stdout in excess of that limit without the output being captured, the subprocess blocks and waits for the pipe buffer to accept more data. Use the `{ stdio: 'ignore' }` option if the output will not be consumed.

The `child_process.spawn()` method spawns the child process asynchronously, without blocking the Node.js event loop.

- `child_process.spawnSync()` is the synchronous version that blocks the event loop until the spawned process either exits or is terminated.

The `child_process.exec()` method spawns a shell and runs a command within that shell, passing the `stdout` and `stderr` to a callback function when complete.

- **Never pass unsanitized user input to this function. Any input containing shell metacharacters may be used to trigger arbitrary command execution.**
- `child_process.execSync()` is the synchronous version that blocks the event loop until the spawned process either exits or is terminated.

The `child_process.execFile()` method is similar to `child_process.exec()` except that it spawns the command directly without first spawning a shell by default. This doesn't work for `.bat` and `.cmd` file in Windows because they cannot be executed without a shell.

- `child_process.execFileSync()` is the synchronous version that blocks the event loop until the spawned process either exits or is terminated.

The `child_process.fork()` method spawns a new Node.js process asynchronously as a `childProcess` object, and invokes a specified module (.js file) with an IPC communication channel established that allows sending messages between parent and child.

- These child processes are independent of the parent, as each process has its own memory and V8 instances, so it is not recommended to spawn large numbers of forks.

Blocking calls are mostly useful for simplifying general-purpose scripting tasks and for simplifying the loading/processing of application configuration at startup with automated shell scripts.

## Worker Threads

The `worker_threads` module enables the use of threads that execute JavaScript in parallel.

- Worker threads are useful for performing CPU-intensive JavaScript operations. They do not help much with I/O-intensive work. The Node.js built-in asynchronous I/O operations are more efficient than Workers can be.
- Unlike `child_process` or `cluster`, `worker_threads` can share memory. They do so by transferring `ArrayBuffer` instances or sharing `SharedArrayBuffer` instances.

## Cluster

A single instance of Node.js runs in a single thread. To take advantage of multi-core systems, the user will sometimes want to launch a cluster of Node.js processes to handle the load.

- The cluster module allows easy creation of child clusters that all share server ports.
- The clusters are spawned using the `child_process.fork()` method, so that they can communicate with the parent via IPC and pass server handles back and forth.
- The cluster module supports two methods of distributing incoming connections:
  - Round-robin (default on every platform except Windows): the master cluster listens on a port, accepts new connections and distributes them across the clusters in a round-robin fashion, with some built-in smarts to avoid overloading a cluster.
  - The second approach is where the master cluster creates the listen socket and sends it to interested clusters. The clusters then accept incoming connections directly. This should be faster in theory, but in practice loads over 70% have been observed using only 2 out of 8 clusters.
- Node.js does not provide routing logic. It is, therefore important to design an application such that it does not rely too heavily on in-memory data objects for things like sessions and login.

Clusters are all separate processes, and can be killed or re-spawned freely, without affecting other clusters. If there are some clusters still alive, the server will continue to accept connections. But if no clusters are alive, existing connections will be dropped and new connections will be refused.

Node.js does not automatically manage the number of clusters, however. It is the application's responsibility to manage the cluster pool based on its own needs.

Although a primary use case for the cluster module is networking, it can also be used for other use cases requiring cluster processes.
