# Node.js - Top 5 features you need to know about

### Short list of the core modules

* __net__    : For creating TCP clients and servers
* __http__   : For creating and consuming HTTP services
* __fs__     : For accessing and manipulating files
* __dns__    : For using the DNS service
* __events__ : For creating event emitters
* __stream__ : For creating streams
* __os__     : For accessing some local operating system statistics
* __assert__ : For assertion test
* __util__   : For miscellaneous utilities

# User modules

### Node.js supports three types of modules:
	1- Core Modules;
	2- User Modules;
	3- Third-party modules

# Node Package Manager (NPM)

###### Node.js has a way of browsing, querying, installing and publishing third-party modules into a central repository, and It's called NPM. NPM stands for Node Package Manager, and it consists of two things:

- A module repository that is fully browsable, accessible at [Node.js](https://npmjs.org/)
- A command-line utility

# The callback pattern

###### Node.js uses the event-driven model of doing I/O, which means that every time that the current process has to talk to the filesystem or the network, It does so in a non-blocking manner.

#### Example of pseudo-code for typical blocking-code:

```javascript

var result = query('SELECT * FROM articles');
console.log('result:', result);

```


###### In event-driven I/O, instead of returning the result of remote operation, you pass a callback that gets involked once that operation is finished.
###### On such platform, the equivalent of doing a database query similar to the previous blocking code would be:

```javascript

query('SELECT * FROM articles', function(result)
{
	console.log('result:', result);
});

```


### Correct blocking version:

```javascript

try
{
	var result = query('SELECT * FROM articles');
	console.log('result:', result);
}
catch( err )
{
	console.error('Error while performing query: ' , err.message);
}

```

### And the equivalent event-driven version would be:

```javascript

query('SELECT * FROM articles', function(err, result)
{
	if( err )
		console.error('error while processing query: ' , err.message);
	else
		console.log('result: ' , result);
});

```


### In this last example, we are witnessing the Node.js callback pattern, which has two characteristics:

* __Callback last__: The callback is the last argument of the function that initates I/O.
* __Error first__  : The callback expects an error as the first argument and the results in the following arguments. If there is no error, the first argument is _undefined_ or _null_. If an error exists, this object should be a JavaScript error instance.



# Chaining I/O

###### When performing chaining, some I/O depends on the result of other I/O; you can chain the two operations
###### by nesting the callback functions. For instance, if you want to verify the size of a file and only read it if it's smaller than 1KB, you could write this into a file named read_file_conditional.js

# Event emitter 

###### The callback pattern is useful when you have I/O operations that have a clear end. If you have an object in which events happen throughout time, the callback pattern is not a good fit. Thankfully, Node.js has a built-in pattern named event emitter.

# Parallelizing I/O

###### Parallelizing I/O is natural in Node.js; You don't need to spawn new threads of execution, simply start two or more I/O operations in parallel. In the following example, we want to make some HTTP requests in parallel to http://www.twitter.com/ .

# Streams

###### A stream represents a source of data read or written throughout time. For instance, you can read the entire contents of a file at once, but if the file is large, this process will take some time and will consume memory. Alternatively, you can read it as a stream, where you get a piece of the file content at a time.


# The writable streams

###### Besides being the source of data, a stream can alternatively or simultaneously be the target of data
###### data-a writable stream. You can write data out to a writable stream, and you can also end one. There are several examples of writable streams in Node.js. You can, for instance, create a writable file stream.


# The duplex streams

###### A stream can be both writable and readable at the same time, permiting both obtaining data from it and writing data to it. An example of such a stream can a TCP connection.

# Stream flow control

###### In Node.js, streams are not only about sending and receiving data but also about controlling the flow of that data.
###### When you write data into a writable stream, that operation is non-blocking, which means that the data may get stored somewhere before it's actually sent out to the underlying resource.
###### If the _write_ operation returns false, the stream will later emit a _drain_ event once the buffer gets flushed.
 
# Piping

###### If you have a _readable_ and _writable_ stream you can connect one to the other using pipe mechanism.

