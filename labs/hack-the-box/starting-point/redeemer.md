# Hack The Box Starting Point: Redeemer

## Objective

The goal of this lab was to practice Redis enumeration, identify an exposed Redis service, connect to it without authentication, and retrieve the flag.

## Target Information

* Platform: Hack The Box
* Machine: Redeemer
* Difficulty: Starting Point / Beginner
* Main Service Explored: Redis
* Open Port Found: `6379`

## Tools Used

* `ping`
* `nmap`
* `redis-cli`
* Basic Redis commands: `ping`, `info`, `keys`, `get`

## Enumeration

I first confirmed that the target machine was reachable.

```bash
ping <target-ip>
```

Command breakdown:

* `ping` checks whether the target responds over the network.
* `<target-ip>` is the IP address assigned by Hack The Box.

The target responded successfully, confirming that the machine was online.

Next, I ran an initial Nmap scan.

```bash
nmap -sV <target-ip>
```

Command breakdown:

* `nmap` scans the target for open ports.
* `-sV` attempts to identify the service and version running on each open port.
* `<target-ip>` is the target machine.

The first scan showed that the host was up, but all 1000 default scanned ports were in ignored states. This meant the machine was reachable, but no open services were found within Nmap’s default top 1000 TCP ports.

Because the default scan did not find an open port, I expanded the scan to check all TCP ports.

```bash
nmap -p- <target-ip>
```

Command breakdown:

* `nmap` is the scanner.
* `-p-` tells Nmap to scan all TCP ports from `1` through `65535`.
* `<target-ip>` is the target machine.

This scan revealed that port `6379` was open and running Redis.

```text
6379/tcp open redis
```

## Service Discovery

Redis is an in-memory database that can store keys and values. Since the Redis port was open, I attempted to connect to it directly.

```bash
redis-cli -h <target-ip>
```

Command breakdown:

* `redis-cli` is the command-line client used to interact with Redis.
* `-h` means host.
* `<target-ip>` is the Redis server I wanted to connect to.

After connecting, I tested whether Redis required authentication.

```redis
ping
```

Command breakdown:

* `ping` is a Redis command that checks whether the Redis server is responding.
* A successful response is `PONG`.

The server responded with:

```text
PONG
```

This confirmed that Redis was accessible without authentication.

## Redis Enumeration

After confirming access, I gathered information about the Redis service.

```redis
info
```

Command breakdown:

* `info` asks Redis for server and database information.
* This can show details such as Redis version, memory usage, connected clients, and keyspace information.

Next, I listed the available keys.

```redis
keys *
```

Command breakdown:

* `keys` lists Redis keys that match a pattern.
* `*` is a wildcard meaning “everything.”

So `keys *` means: show all keys in the current Redis database.

This revealed a key named:

```text
flag
```

## Flag Retrieval

Since Redis stores data as key-value pairs, I used the `get` command to retrieve the value stored in the `flag` key.

```redis
get flag
```

Command breakdown:

* `get` retrieves the value stored at a specific Redis key.
* `flag` is the key name I found during enumeration.

The flag was successfully retrieved and submitted on Hack The Box.

## Key Takeaways

* Nmap’s default scan checks the top 1000 TCP ports, not every possible port.
* If a target is reachable but no open ports are found, a full port scan may reveal services running on less common ports.
* Redis commonly runs on port `6379`.
* `redis-cli` can be used to connect to and interact with a Redis service.
* A `PONG` response confirms that Redis is reachable and responding.
* If Redis does not require authentication, it may be possible to enumerate keys and retrieve stored values.
* Redis data is commonly accessed using commands like `info`, `keys *`, and `get`.

## Summary

In this lab, I practiced expanding Nmap scans beyond the default port range, identifying Redis on port `6379`, connecting to Redis using `redis-cli`, confirming unauthenticated access, enumerating available keys, and retrieving the flag.
