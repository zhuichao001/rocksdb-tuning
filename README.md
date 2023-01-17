## Rocksdb 参数调优

### MemoryTable
- write_buffer_size:
  适当增大该参数可以减小写放大
- max_write_buffer_number:
  具有一定的削峰作用，当全部memtable都写满，flush速度跟不上写入速率，就会造成停写；如果内存充足或是机械磁盘，建议调大该值
- min_write_buffer_number_to_merge
  flush的触发条件，同时对多个memtable进行归并排序，好处是可以减小写放大，但又可能增加读放大；经过实际测试，该值设为2或3较好

### Block/Block Cache
Block是sstable的基本存储单温；Block Cache用来缓存Block，可以加速读操作和Compaction速度
- blockr_ size
  一般设置为32k、64k，调大可以减小空间放大，但是不利于缓存命中，增加读放大
- block_cache_size
 根据实际的内存容量来设，建议总的block cache空间占内存的1/4到1/3，调大该值对该CF的读性能有明显提升
### Compaction
- compaction_style
默认Leveld Compaction
- target_file_size_base
L1层单个sstable文件的大小阈值，默认值为64MB；逐上各级，阈值会乘以因子target_file_size_multiplier(默认为1)。增大该值可以降低Compaction的频率，减少写放大，但是也会造成空间放大和读放大（旧数据不能及时清理）
- max_bytes_for_level_base
L1层(base)的数据总大小阈值，默认值为256MB;逐上各级，层大小会乘以因子max_bytes_for_level_multiplier(默认值10)
- level_compaction_dynamic_level_bytes
该参数打开后，保持LSM树的正三角形形态，逐层的阈值大小会动态调整，可以减少写放大
### 通用参数
- max_open_files
RocksDB实例能打开的最大文件数, 默认为-1，表示不受限制；由于对应sst的索引和布隆过滤器会驻守内存，并占用文件描述符，所以此值不宜太小，否则影响索引和布隆过滤器的正常加载，拖累读性能
- max_background_compactions
后台负责flush和compaction的最大并发线程数，默认为1；如果CPU核数富余，建议调大
