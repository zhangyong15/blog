# Paddle的几个问题

* paddle路径不能重复
  如使用paddle_data/{20170821,20170822}/, 20170821和20170822均有part-00000，若发生文件命名重复时，paddle会不断覆盖本地文件，导致真正训练只使用其中
  的一份part。
  解决方案：本地先进行训练数据merge，然后再提交训练
  
* Paddle会通过dataprovider将所有的训练数据下载到MPI的磁盘，然后再开始训练。

* Paddle内部实现parameter server，通讯独立于MPI。一个paddle任务需要独占MPI端口，只要端口有重复，任务会失败。

* 关于pool_size， batch_size, trainer_count, shuffle
  trainer_count为启动的线程数目，min_batch_size = batch_size / trainer_count
  pool_size在内存允许前提下，尽量设大，paddle运行时会先填充pool_size，然后shuffle，分割成每个batch_size训练。
  trainer_count的设置一般不建议超过CPU数目，batch_size需要小于pool_size，可以为一个倍数关系
  训练效率与pool_size相关， 与batch_size关系未确定？
  
* Paddle支持大规模离散DNN问题比较多？
