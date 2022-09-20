[TOC]

## 潘多拉STM32L475开发板使用J-Link作为RT-Thread的console接口

---

#### 1、创建工程，调试器选择J-Link，接口选择SWD

![image-20220830084715047](https://img-blog.csdnimg.cn/img_convert/0c6f5ec5e16fd7a1aeffaa57d59d6415.png)

#### 2、添加segger_rtt软件包

![image-20220830084812929](https://img-blog.csdnimg.cn/img_convert/2155b6aaea2e31f17cdcb078d316954f.png)

#### 3、Settings->内核->内核设备对象->为rt_kprintf使用控制台，修改控制台设备名称为`jlinkRtt`

![image-20220830085026967](https://img-blog.csdnimg.cn/img_convert/198907c53285b4f66f4cae8338af965b.png)

#### 4、打开文件kservice.c（路径：/rt-thread/src/kservice.c），定位找到rt_console_set_device函数，将下面这个函数放在rt_console_set_device这个函数的第一行

```c
rt_hw_jlink_rtt_init();
```

![image-20220830085538537](https://img-blog.csdnimg.cn/img_convert/7ae8b48a7e0eefdb686f88bd579c72a1.png)

> 解释：由于目前console是在rt_hw_jlink_rtt_init();中初始化的，所以需要把`rt_console_set_device(RT_CONSOLE_DEVICE_NAME);`放到`rt_hw_jlink_rtt_init();`后面

#### 5、编写测试代码

![image-20220830085943649](https://img-blog.csdnimg.cn/img_convert/ec90a9d8a48e6b35b62d21d71b1581a7.png)

关于segger_rtt函数API详细请看[supperthomas-wiki](https://supperthomas-wiki.readthedocs.io/en/latest/DEBUG/01_SEGGER_RTT/SEGGER_RTT.html#id1)

![image-20220830090040247](https://img-blog.csdnimg.cn/img_convert/f12385d56e7df6dab301d62fe342cd0a.png)

#### 6、下载测试

打开J-Link RTT Viewer，选择开发板型号并选择Auto Detection

[J-Link RTT Viewer官网下载地址](https://www.segger.com/products/debug-probes/j-link/tools/rtt-viewer/)

![image-20220830090453201](https://img-blog.csdnimg.cn/img_convert/f261879fe4180c8c13443a1050b59bf4.png)

查看结果，成功打印调试信息即为成功：

![image-20220830090328673](https://img-blog.csdnimg.cn/img_convert/7bf04f5117dce32c2d38e53e745e12db.png)

终端命令输出

![](https://img-blog.csdnimg.cn/img_convert/7bf04f5117dce32c2d38e53e745e12db.png)
