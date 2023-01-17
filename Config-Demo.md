配置：16核CPU，32G内存，1T SSD硬盘
## DB Options
```
allow_os_buffer = false
max_open_files = -1
disable_wal = false
enable_pipelined_write = true
max_background_flushes = 4
max_background_compactions = 16
max_subcompactions = 4
background_rate_limit = 160M
background_rate_limit_fairness = 10
background_rate_limit_mode = 0  #0:write 1:read 2:all
background_rate_limit_auto_tune = false
avoid_unnecessary_blocking_io = true
```

## Column Family Options
```
write_buffer_size = 512MB
max_write_buffer_number = 4
min_write_buffer_number_to_merge = 2

target_file_size_base = 64MB
max_bytes_for_level_base = 4096MB
num_levels = 6

block_size = 32KB
block_cache_size = 4096MB

#官方推荐前面n-1层的压缩首选用LZ4，其次Snappy
compression = 4
#最底层首选用ZStand，其次Zlib
bottommost_compression = 7

cache_index_and_filter_blocks = 1
pin_l0_filter_and_index_blocks_in_cache = 1
partition_filters = 1

level0_file_num_compaction_trigger = 8
level0_slowdown_writes_trigger = 24
level0_stop_writes_trigger = 40
```
