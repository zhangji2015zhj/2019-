# 2019-
2019秋招笔试

# 线程同步
   * 互斥量 mutex： 访问前加锁，访问后释放
   * 避免死锁 试图对同一互斥量加锁两次，陷入死锁；多个互斥量互相阻塞；ptherad_mutex_trylock 避免阻塞
   * 读写锁 类似于互斥量。允许高并发 （读锁，写锁，不加锁） 共享读，单一写
   * 条件变量 线程的一种同步机制，与互斥量一起使用时，允许线程以无竞争地方式等待特定条件发生。
   

   