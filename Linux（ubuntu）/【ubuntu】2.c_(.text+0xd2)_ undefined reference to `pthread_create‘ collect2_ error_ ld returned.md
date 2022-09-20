## 编译错误信息：2.c:(.text+0xd2): undefined reference to `pthread_create‘ collect2: error: ld returned 1 exit status


>代码部分：
```
#include<stdio.h>
#include<stdlib.h>
#include<sys/types.h>
#include<sys/stat.h>
#include<unistd.h>
#include<fcntl.h>
#include<string.h>
#include<pthread.h>

char buf[200]={0};

void *func(void *arg)
{
	while(1)
	{
		memset(buf,0,sizeof(buf));//初始化内存函数
		printf("before keyboard read.\n");
		read(0,buf,10);
		printf("read by keyboard is [%s]\n",buf);
	}
}

int main(void)
{
	pid_t pid = -1;
	int fd = -1;
	char buf[200]={0};
	int ret = -1;
	
	pthread_t th = -1;
	
	ret = pthread_create(&th,NULL,func,NULL); //创建一个新进程
	if(ret != 0)
	{
		printf("pthread_created eror.\n");
		return -1;
	}
	
	fd = open("/dev/input/mouse0",O_RDWR);
	if(fd < 0)
	{ 
		perror("open");
		return -1;
	}
	while(1)
	{
		memset(buf,0,sizeof(buf));//初始化内存函数
		printf("before mouse read.\n");
		read(fd,buf,10);
		printf("read by mouse is [%s]\n",buf);
	}

	
	return 0;
}
```

>ubuntu环境下运行

![报错](https://img-blog.csdnimg.cn/cfbdcffa749f446ca709e3c4ed1b6994.png)  
>解决方案：
>在编译文件命令后加上-lphread  

>示范：gcc 2.c -lpthread  
>
![在这里插入图片描述](https://img-blog.csdnimg.cn/a000dce6b3f84d95a9d89ecfc749246d.png)

​	 
