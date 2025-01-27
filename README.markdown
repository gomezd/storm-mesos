# Build of storm-mesos using mesos-0.17.0 and storm-0.9.1-incubating

## Running storm on mesos

- Get Zookeeper

See http://zookeeper.apache.org/doc/trunk/zookeeperStarted.html#sc_InstallingSingleMode

- Download and build mesos

```bash
wget http://www.apache.org/dist/mesos/0.17.0/mesos-0.17.0.tar.gz
tar -zxf mesos-0.17.0.tar.gz

# Change working directory.
$ cd mesos-0.17.0

# Configure and build.
$ mkdir build
$ cd build
$ ../configure
$ make

# Run test suite.
$ make check

# Install (***Optional***).
$ make install
```
see http://mesos.apache.org/gettingstarted/

- Start mesos
```bash
# mesos master
mesos-0.17.0/build/bin/mesos-master.sh --zk=zk://localhost:2181/mesos &

# mesos slave
mesos-0.17.0/build/bin/mesos-slave.sh --master=zk://localhost:2181/mesos &
```

You can see the mesos UI in localhost:5050

- Configure `conf/storm.yaml`
```yaml
## Default configuration for standalone mode (every daemons on one node with default settings)

# Path to mesos distribution built properly
# java.library.path: "native:/path/to/mesos-0.17.0/build/.libs"

# hostname:port of the mesos master node
mesos.master.url: "zk://localhost:2181/mesos"

# in cluster ENV, change it to a globally accessible directory (HDFS or NFS etc.)
mesos.executor.uri: "/path/to/storm-mesos-0.9.1-incubating.tgz"

# hostname:port of zookeeper nodes (default port 2181)
storm.zookeeper.servers:
- "localhost"

# hostname of nimbus node
nimbus.host: "localhost"

# full path of storm local working directory
storm.local.dir: "/usr/local/storm-local"
```

- Start storm
```bash
bin/storm-mesos nimbus &
bin/storm supervisor &
bin/storm ui
```
You can see the storm ui on localhost:8080 and you will see storm registered as a mesos framework.

- Download storm-starter and send topologies to the storm cluster
```bash
apache-storm-0.9.1-incubating/bin/storm jar storm-starter-0.0.1-SNAPSHOT.jar storm.starter.WordCountTopology count 
```

-------------------


Storm is a distributed realtime computation system. Similar to how Hadoop provides a set of general primitives for doing batch processing, Storm provides a set of general primitives for doing realtime computation. Storm is simple, can be used with any programming language, [is used by many companies](https://github.com/nathanmarz/storm/wiki/Powered-By), and is a lot of fun to use!

The [Rationale page](https://github.com/nathanmarz/storm/wiki/Rationale) on the wiki explains what Storm is and why it was built. [This presentation](http://vimeo.com/40972420) is also a good introduction to the project.

Storm has a website at [storm-project.net](http://storm-project.net). Follow [@stormprocessor](https://twitter.com/stormprocessor) on Twitter for updates on the project.

## Documentation

Documentation and tutorials can be found on the [Storm wiki](http://github.com/nathanmarz/storm/wiki).

## Getting help

__NOTE:__ The google groups account storm-user@googlegroups.com is now officially deprecated in favor of the Apache-hosted user/dev mailing lists.

### Storm Users
Storm users should send messages and subscribe to [user@storm.incubator.apache.org](mailto:user@storm.incubator.apache.org).

You can subscribe to this list by sending an email to [user-subscribe@storm.incubator.apache.org](mailto:user-subscribe@storm.incubator.apache.org). Likewise, you can cancel a subscription by sending an email to [user-unsubscribe@storm.incubator.apache.org](mailto:user-unsubscribe@storm.incubator.apache.org).

You can view the archives of the mailing list [here](http://mail-archives.apache.org/mod_mbox/incubator-storm-user/).

### Storm Developers
Storm developers should send messages and subscribe to [dev@storm.incubator.apache.org](mailto:dev@storm.incubator.apache.org).

You can subscribe to this list by sending an email to [dev-subscribe@storm.incubator.apache.org](mailto:dev-subscribe@storm.incubator.apache.org). Likewise, you can cancel a subscription by sending an email to [dev-unsubscribe@storm.incubator.apache.org](mailto:dev-unsubscribe@storm.incubator.apache.org).

You can view the archives of the mailing list [here](http://mail-archives.apache.org/mod_mbox/incubator-storm-dev/).

### Which list should I send/subscribe to?
If you are using a pre-built binary distribution of Storm, then chances are you should send questions, comments, storm-related announcements, etc. to [user@storm.apache.incubator.org](user@storm.apache.incubator.org).

If you are building storm from source, developing new features, or otherwise hacking storm source code, then [dev@storm.incubator.apache.org](dev@storm.incubator.apache.org) is more appropriate.

### What will happen with storm-user@googlegroups.com?
All existing messages will remain archived there, and can be accessed/searched [here](https://groups.google.com/forum/#!forum/storm-user).

New messages sent to storm-user@googlegroups.com will either be rejected/bounced or replied to with a message to direct the email to the appropriate Apache-hosted group.

### IRC
You can also come to the #storm-user room on [freenode](http://freenode.net/). You can usually find a Storm developer there to help you out.

## License

Licensed to the Apache Software Foundation (ASF) under one
or more contributor license agreements.  See the NOTICE file
distributed with this work for additional information
regarding copyright ownership.  The ASF licenses this file
to you under the Apache License, Version 2.0 (the
"License"); you may not use this file except in compliance
with the License.  You may obtain a copy of the License at

  http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
KIND, either express or implied.  See the License for the
specific language governing permissions and limitations
under the License.


## Project lead

* Nathan Marz ([@nathanmarz](http://twitter.com/nathanmarz))

## Committers

* James Xu ([@xumingming](https://github.com/xumingming))
* Jason Jackson ([@jason_j](http://twitter.com/jason_j))
* Andy Feng ([@anfeng](https://github.com/anfeng))
* Flip Kromer ([@mrflip](https://github.com/mrflip))
* David Lao ([@davidlao2k](https://github.com/davidlao2k))
* P. Taylor Goetz ([@ptgoetz](https://github.com/ptgoetz))

## Contributors

* Christopher Bertels ([@bakkdoor](http://twitter.com/bakkdoor))
* Michael Montano ([@michaelmontano](http://twitter.com/michaelmontano))
* Dennis Zhuang ([@killme2008](https://github.com/killme2008))
* Trevor Smith ([@trevorsummerssmith](https://github.com/trevorsummerssmith))
* Ben Hughes ([@schleyfox](https://github.com/schleyfox))
* Alexey Kachayev ([@kachayev](https://github.com/kachayev))
* Haitao Yao ([@haitaoyao](https://github.com/haitaoyao))
* Dan Dillinger ([@ddillinger](https://github.com/ddillinger))
* Kang Xiao ([@xiaokang](https://github.com/xiaokang))
* Gabriel Grant ([@gabrielgrant](https://github.com/gabrielgrant))
* Travis Wellman ([@travisfw](https://github.com/travisfw))
* Kasper Madsen ([@KasperMadsen](https://github.com/KasperMadsen))
* Michael Cetrulo ([@git2samus](https://github.com/git2samus))
* Thomas Jack ([@tomo](https://github.com/tomo))
* Nicolas Yzet ([@nicoo](https://github.com/nicoo))
* Fabian Neumann ([@hellp](https://github.com/hellp))
* Soren Macbeth ([@sorenmacbeth](https://github.com/sorenmacbeth))
* Ashley Brown ([@ashleywbrown](https://github.com/ashleywbrown))
* Guanpeng Xu ([@herberteuler](https://github.com/herberteuler))
* Vinod Chandru ([@vinodc](https://github.com/vinodc))
* Martin Kleppmann ([@ept](https://github.com/ept))
* Evan Chan ([@velvia](https://github.com/velvia))
* Sjoerd Mulder ([@sjoerdmulder](https://github.com/sjoerdmulder))
* Yuta Okamoto ([@okapies](https://github.com/okapies))
* Barry Hart ([@barrywhart](https://github.com/barrywhart))
* Sergey Lukjanov ([@Frostman](https://github.com/Frostman))
* Ross Feinstein ([@rnfein](https://github.com/rnfein))
* Junichiro Takagi ([@tjun](https://github.com/tjun))
* Bryan Peterson ([@Lazyshot](https://github.com/Lazyshot))
* Sam Ritchie ([@sritchie](https://github.com/sritchie))
* Stuart Anderson ([@emblem](https://github.com/emblem))
* Robert Evans ([@revans2](https://github.com/revans2))
* Lorcan Coyle ([@lorcan](https://github.com/lorcan))
* Derek Dagit ([@d2r](https://github.com/d2r))
* Andrew Olson ([@noslowerdna](https://github.com/noslowerdna))
* Gavin Li ([@lyogavin](https://github.com/lyogavin))
* Tudor Scurtu ([@tscurtu](https://github.com/tscurtu))
* Homer Strong ([@strongh](https://github.com/strongh))
* Sean Melody ([@srmelody](https://github.com/srmelody))
* Jake Donham ([@jaked](https://github.com/jaked))
* Ankit Toshniwal ([@ankitoshniwal](https://github.com/ankitoshniwal))

## Acknowledgements

YourKit is kindly supporting open source projects with its full-featured Java Profiler. YourKit, LLC is the creator of innovative and intelligent tools for profiling Java and .NET applications. Take a look at YourKit's leading software products: [YourKit Java Profiler](http://www.yourkit.com/java/profiler/index.jsp) and [YourKit .NET Profiler](http://www.yourkit.com/.net/profiler/index.jsp).
