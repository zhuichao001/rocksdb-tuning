## MemoryTable
- write_buffer_size:
  适当增大该参数可以减小写放大
- max_write_buffer_number:
  具有一定的削峰作用，当全部memtable都写满，flush速度跟不上写入速率，就会造成停写；如果内存充足或是机械磁盘，建议调大该值
- min_write_buffer_number_to_merge
  flush的触发条件，同时对多个memtable进行归并排序，好处是可以减小写放大，但又可能增加读放大；经过实际测试，该值设为2或3较好
