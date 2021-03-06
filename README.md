etcd.erl
========

Erlang bindings for [etcd](https://github.com/coreos/etcd) key value store.

## Usage
### start
```erlang
etcd:start()
```
### set
```erlang
{ok, Response} = etcd:set("http://localhost:4001", "/message", "Hello world", 400).
```
``"/message"`` is the key and ``"Hello world"`` is the value. ``400`` is the timeout.
### get
```erlang
{ok, Response} = etcd:get("http://localhost:4001", "/message", infinity).
```
### test and set
```erlang
etcd:set("http://localhost:4001", "/message", "one", infinity),
{ok, Response} = etcd:test_and_set("http://localhost:4001", "/message", "one", "two", infinity).
```
Directories are also supported:
```erlang
{ok, Response1} = etcd:set("http://localhost:4001", "/foo/message1", "Hello day", infinity),
{ok, Response2} = etcd:set("http://localhost:4001", "/foo/message2", "Hello night", infinity),
{ok, ResponseList} = etcd:get("http://localhost:4001", "/foo", infinity).
```
### delete
```erlang
etcd:set("http://localhost:4001", "/message", "Hello world", infinity),
etcd:delete("http://localhost:4001", "/message", infinity).
```
### watch
```erlang
Result = etcd:watch("http://localhost:4001", "/foo", infinity),
```
Watch for commands at index ``42``:
```erlang
Result = etcd:watch("http://localhost:4001", "/foo", 42, infinity),
```
