## Block/Block Cache
Block是sstable的基本存储单温；Block Cache用来缓存Block，可以加速读操作和Compaction速度
- blockr_ size
  一般设置为32k、64k，调大可以减小空间放大，但是不利于缓存命中，增加读放大
- block_cache_size
 根据实际的内存容量来设，建议总的block cache空间占内存的1/4到1/3，调大该值对该CF的读性能有明显提升
