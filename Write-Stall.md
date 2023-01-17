RocksDB在Flush或Compaction时，速度跟不上新写入速率，存储引擎启动保护机制:延迟写或者禁写。
## Too many memtables
- 写限速
  将要Flush的memtables大于等于max_write_buffer_number-1, write会被限速
- 禁写
  memtable个数大于等于max_write_buffer_number且写满, 触发禁写，等到Flush完成后允许继续写入

## Too many Level-0 SST files
- 写限速
  L0文件数量达到level0_slowdown_writes_trigger, 触发写限速
- 禁写
  L0文件数量达到Level0_stop_writes_trigger，触发禁写

## Too many pending compaction bytes
- 写限速
  等待Compaction的SST个数大于该值则触发写限速
  ```
  level0_slowdown_writes_trigger = {}
  ```

- 禁写
  等待Compaction的SST个数大于该值则触发禁写
  ```
  level0_stop_writes_trigger = {}
  ```
