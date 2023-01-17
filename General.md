## 通用参数
- max_open_files
RocksDB实例能打开的最大文件数, 默认为-1，表示不受限制；由于对应sst的索引和布隆过滤器会驻守内存，并占用文件描述符，所以此值不宜太小，否则影响索引和布隆过滤器的正常加载，拖累读性能
- max_background_compactions
后台负责flush和compaction的最大并发线程数，默认为1；如果CPU核数富余，建议调大
