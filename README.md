## Rocksdb 性能调优

- Compaction的触发条件
  - witch wal：当 WAL 的文件大小超过阈值时, 触发Flush
  - writer buffer full：当 memtable 写满时, 触发Flush
  - schedule compaction
    - 手工compaction
    - Ln-1的大小达到阈值的上限
    - Ln-1的查找Miss达到上限
