首先在lab1的基础上可能会出现一些问题,具体体现在 [问题出处](https://blog.csdn.net/ChloeWeever/article/details/144327611?spm=1001.2014.3001.5502)

可以选择包装一次`thread_yield`调用
```c
void thread_try_yield(void) {
  if (!list_empty(&ready_list) && thread_current() != idle_thread)
    thread_yield();
}
```
[解决方案出处](https://stackoverflow.com/questions/52472084/pintos-userprog-all-tests-fail-is-kernel-vaddr)
当然也可以选择重新开一个pintos (以下基于一个新的pintos源码)
[更好的pintos指导](https://pkuflyingpig.gitbook.io/pintos)

需要在usrprog的目录下去重新构建项目并且将pintos的loader 和 kernel都重新指向这个新的.整个项目基于pintos的文件系统,所以要新建一个filesys.dsk,以下是一个测试
```bash
$ pintos-mkdisk filesys.dsk --filesys-size=2
$ pintos -p ../../examples/echo -a echo -- -f -q run 'echo PKUOS'
```
但是会发现最后执行是echo PKUOS整个字符串作为一个程序一起执行的,而不是echo,而pintos在这里的第一个任务就是完成整个程序调用的参数分离.
接下来看
