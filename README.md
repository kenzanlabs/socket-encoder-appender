A [Logback](http://logback.qos.ch/) Appender that encodes logs using
an [Encoder](http://logback.qos.ch/manual/encoders.html), and sends
the result to a remote host over TCP.

Why not use the normal SocketAppender?
--------------------------------------

Strangely, the default logback [Socket
Appender](http://logback.qos.ch/manual/appenders.html#SocketAppender)
doesn't give you control over how logs are encoded. Rather, it uses
java object serialization and sends the result to a remote TCP socket,
where it assumed you will deserialize messages back into a running JVM
process.

In my work on [logback-gelf](https://github.com/Moocar/logback-gelf),
I needed to encode messages into GELF json before sending over TCP.
Much to my annoyance, SocketAppender wouldn't allow that. Thus, this
library.

Dependency information
-----------------------------------

Latest version:

```xml
<dependency>
  <groupId>me.moocar</groupId>
  <artifactId>socket-encoder-appender</artifactId>
  <version>0.1beta1</version>
</dependency>
```

Usage
-----

See
[logback-gelf TCP configuration](https://github.com/Moocar/logback-gelf/tree/the-great-appender-rejig#tcp)
For an example of how to configure this appender. Note, that a null
delimeter (\0 character) will be added to the end of every sent log.

### Configuration

* **remoteHost**: The remote server host name to send log messages to
  (DNS or IP). Default: `"localhost"`
* **port**: The remote server port. Required
* **queueSize**: The number of log to keep in memory while the remote
  server can't be reached. Default: `128`
* **acceptConnectionTimeout**: Milliseconds to wait for a connection
  to be established to the server before failing. Default: `1000`
