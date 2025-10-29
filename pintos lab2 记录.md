首先在lab1的基础上可能会出现一些问题,具体体现在 [地址](https://blog.csdn.net/ChloeWeever/article/details/144327611?spm=1001.2014.3001.5502)

可以选择包装一次`thread_yield`调用
```c
void thread_try_yield(void) {
  if (!list_empty(&ready_list) && thread_current() != idle_thread)
    thread_yield();
}
```
[出处](https://stackoverflow.com/questions/52472084/pintos-userprog-all-tests-fail-is-kernel-vaddr)
当然也可以选择重新开一个pintos (以下基于一个新的pintos源码)

