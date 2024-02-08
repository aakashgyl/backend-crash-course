# Redis Commands

### 1. Key-Value Operations:
```
redislabs.com:18787> SET mykey "Hello, Redis!"
OK

redislabs.com:18787> GET mykey
"Hello, Redis!"

redislabs.com:18787> EXISTS mykey
(integer) 1

redislabs.com:18787> KEYS *
1) "mykey"

redislabs.com:18787> DEL mykey
(integer) 1

redislabs.com:18787> EXISTS mykey
(integer) 0

redislabs.com:18787> KEYS *
(empty array)
```

### 2. String Operations:
```
redislabs.com:18787> SET mykey "Hello, Redis!"
OK

redislabs.com:18787> APPEND mykey ", how are you?"
(integer) 27

redislabs.com:18787> STRLEN mykey
(integer) 27

redislabs.com:18787> GET mykey
"Hello, Redis!, how are you?"
```

### 3. List Operations:
```
redislabs.com:18787> LPUSH mylist "left-push-1" "left-push-2"
(integer) 2

redislabs.com:18787> LRANGE mylist 0 -1
1) "left-push-2"
2) "left-push-1"

redislabs.com:18787> RPUSH mylist "right-push-1" "right-push-2"
(integer) 4

redislabs.com:18787> LRANGE mylist 0 -1
1) "left-push-2"
2) "left-push-1"
3) "right-push-1"
4) "right-push-2"

redislabs.com:18787> LPOP mylist
"left-push-2"

redislabs.com:18787> RPOP mylist
"right-push-2"
```

### 4. Set Operations:
```
// Add to Set
redislabs.com:18787> SADD myset "apple" "orange" "banana"
(integer) 3

// Set Members
redislabs.com:18787> SMEMBERS myset
1) "banana"
2) "apple"
3) "orange"

// Is Member of Set?
redislabs.com:18787> SISMEMBER myset "apple"
(integer) 1

redislabs.com:18787> SISMEMBER myset "appleaaa"
(integer) 0

// Remove from Set
redislabs.com:18787> SREM myset "orange"
(integer) 1

redislabs.com:18787> SMEMBERS myset
1) "banana"
2) "apple"

// Add new member to Set
redislabs.com:18787> SADD myset "guava"
(integer) 1

redislabs.com:18787> SMEMBERS myset
1) "banana"
2) "guava"
3) "apple"

redislabs.com:18787> SADD myset "guava"
(integer) 0
```

### 5. Sorted Set Operations:
```
// Format -> score value (sorted on basis of score)
redislabs.com:18787> ZADD myscores 10 "Alice" 8 "Bob" 15 "Charlie"
(integer) 3

redislabs.com:18787> ZRANGE myscores 0 -1 WITHSCORES
1) "Bob"
2) "8"
3) "Alice"
4) "10"
5) "Charlie"
6) "15"

redislabs.com:18787> ZSCORE myscores "Alice"
"10"

// Remove member
redislabs.com:18787> ZREM myscores "Bob"
(integer) 1

redislabs.com:18787> ZRANGE myscores 0 -1 WITHSCORES
1) "Alice"
2) "10"
3) "Charlie"
4) "15"

redislabs.com:18787> ZRANGE myscores 0 -1
1) "Alice"
2) "Charlie"
```

### 6. Hash Operations:
```
redislabs.com:18787> HSET user:id:123 username "john_doe" password "pwd"
(integer) 2

redislabs.com:18787> HGETALL user:id:123
1) "username"
2) "john_doe"
3) "password"
4) "pwd"

redislabs.com:18787> HGET user:id:123 username
"john_doe"

redislabs.com:18787> HSET user:id:123 website "domain.com"
(integer) 1

redislabs.com:18787> HGETALL user:id:123
1) "password"
2) "pwd"
3) "username"
4) "john_doe"
5) "website"
6) "domain.com"

redislabs.com:18787> HDEL user:id:123 username
(integer) 1

redislabs.com:18787> HGET user:id:123 username
(nil)
```

### 7. Increment Decrement Operations:
```
redislabs.com:18787> incr counter
(integer) 1
redislabs.com:18787> incr counter
(integer) 2
redislabs.com:18787> incr counter
(integer) 3
redislabs.com:18787> incr counter
(integer) 4
redislabs.com:18787> decr counter
(integer) 3
redislabs.com:18787> decr counter
(integer) 2
redislabs.com:18787> decr counter
(integer) 1
redislabs.com:18787> decr counter
(integer) 0
redislabs.com:18787> decr counter
(integer) -1
redislabs.com:18787> decr counter
(integer) -2
```

### 8. TTL Operations:
```
// set keyname and specify TTL (in seconds)
redislabs.com:18787> SET key_name "value" EX 3600
OK

// specify ttl (in seconds) for existing key
redislabs.com:18787> EXPIRE key_name 60
(integer) 1

// check remaining time (in seconds)
redislabs.com:18787> TTL key_name
(integer) 51

redislabs.com:18787> PERSIST key_name
(integer) 1

// ttl no longer applicable
redislabs.com:18787> TTL key_name
(integer) -1
```

### 9. Other Operations:
```
redislabs.com:18787> keys *
1) "user:id:123"
2) "myscores"
3) "myset"
4) "mylist"

redislabs.com:18787> FLUSHALL
OK

redislabs.com:18787> keys *
(empty array)

redislabs.com:18787> PING
PONG

redislabs.com:18787> INFO
# Server
redis_version:6.2.6
redis_git_sha1:00000000
redis_git_dirty:0
redis_build_id:0000000000000000000000000000000000000000
redis_mode:standalone
os:Linux 5.4.0-1080-aws x86_64
arch_bits:64
multiplexing_api:epoll
gcc_version:7.5.0
process_id:12133986
run_id:dd75ec1bcc4ae818c1eb7241bd74d05adcfc8174
tcp_port:18787
server_time_usec:1707329898000000
uptime_in_seconds:1707329898
uptime_in_days:19760
hz:10
lru_clock:0
config_file:

# Clients
connected_clients:1
client_longest_output_list:0
client_biggest_input_buf:0
blocked_clients:0
maxclients:30
cluster_connections:0

# Memory
used_memory:2391376
used_memory_human:2.28M
used_memory_rss:2391376
used_memory_peak:3162208
used_memory_peak_human:3.1M
used_memory_lua:32768
mem_fragmentation_ratio:1
mem_allocator:jemalloc-5.1.0

# Persistence
loading:0
rdb_changes_since_last_save:41
rdb_bgsave_in_progress:0
rdb_last_save_time:1707327611
rdb_last_bgsave_status:ok
rdb_last_bgsave_time_sec:0
rdb_current_bgsave_time_sec:-1
aof_enabled:0
aof_rewrite_in_progress:0
aof_rewrite_scheduled:0
aof_last_rewrite_time_sec:-1
aof_current_rewrite_time_sec:-1
aof_last_bgrewrite_status:ok
aof_last_write_status:ok

# Stats
total_connections_received:1
total_commands_processed:75
instantaneous_ops_per_sec:0
total_net_input_bytes:183178
total_net_output_bytes:3401207
instantaneous_input_kbps:0.08
instantaneous_output_kbps:1.60
rejected_connections:0
sync_full:0
sync_partial_ok:0
sync_partial_err:0
expired_keys:0
evicted_keys:0
keyspace_hits:50
keyspace_misses:12
pubsub_channels:0
pubsub_patterns:0
latest_fork_usec:0
migrate_cached_sockets:0
total_forks:0
total_error_replies:0

# Replication
role:master
connected_slaves:0
master_repl_offset:0
repl_backlog_active:0
repl_backlog_size:1048576
repl_backlog_first_byte_offset:0
repl_backlog_histlen:0

# CPU
used_cpu_sys:0.00
used_cpu_user:0.00
used_cpu_sys_children:0.00
used_cpu_user_children:0.00
used_cpu_sys_main_thread:0.00
used_cpu_user_main_thread:0.00

# Cluster
cluster_enabled:0

# Keyspace
db0:keys=4,expires=0,avg_ttl=0
```
