(1)新增的用户看起来正常，但是移除用户的时候，貌似第一个用户被替换了


(2)将客户管理的方式修改成直接加锁的方式，在处理完客户的请求包之后直接在响应线程内部将数据发送完成
NOTE： 在这里需要注意的地方是处理线程和epoll事件处理线程不在同一个线程，故当使用客户对象的时候需要加锁，
但是使用只能指针的时候有一个好处，如果epoll中将客户删除了，此时处理线程将客户对象取出来了，那么在处理线程
保持着这个客户对象的最后引用计数，在处理线程使用客户对象不会出错，不过在发送的时刻报错后即可彻底移除这个
客户对象