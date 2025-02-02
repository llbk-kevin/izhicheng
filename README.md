# i至诚自动化打卡

## 源码开源，仅用于学习

### window自动定时使用 Windows 任务调度程序，可以自行百度

### 出现 bug 请在 issue 提交问题
```
2021.11.28 更新：感谢 @miscdec 的帮助，实现在 GitHub Action 上的学号的批量打卡
2021.11.26 更新：修复 chrome 版本更新导致失效，使用 webdriver 自动更新一劳永逸 
2021.11.16 更新：感谢 @R-YaTian 的帮助，可以在顺利在凌晨进行打卡
2021.10.24 更新：更改无服务器可用版本 只需要 GitHub 账号 使用方法见文章末尾
2021.10.04 更新：更改打卡链接地址
2021.07.13 更新：优化在家代码，可更改地区
2021.06.08 更新：去除广告弹窗
2021.03.30 更新：重构代码减少报错
2021.03.26 更新：修复了在校代码bug
2021.03.19 更新：修复了windows在校代码错误
2021.03.19 更新：修复了批量打卡导致页面加载不出
2021.03.02 更新：新增在校版，只需要学号
2021.02.15 更修：增加了批量填报
2021.02.15 更新：增加错误日志发送邮件
2021.02.13 更新：增加了windows版并修复了BUG
```

### 零、环境准备

centos7云服务准备：https://developer.aliyun.com/adc/student/

环境准备：https://www.cnblogs.com/Lin1031/p/14187135.html

博客园地址：https://www.cnblogs.com/Lin1031/p/14187137.html


### 一、在根目录下新建一个py文件
```
cd
touch tianbiao.py
vim tianbiao.py
```
### 二、编辑python程序(注意，要修改path地址为本地，driverchrome路径)


#### 开源不易，希望GitHub给个star
#### GitHub地址：https://github.com/Lin1031/izhicheng


### 三、在根目录下创建一个脚本
```
cd 
touch my.sh
vim my.sh
```
### 四、编辑脚本内容（路径修改为本地py文件路径，学号处修改为自己的学号）
```
#!/bin/bash
. /etc/profile
. ~/.bash_profile
python的绝对路径 /root/tianbiao.py 学号 省份 市 区（主要要和i至诚上面一模一样）
```
![](https://img2020.cnblogs.com/blog/1535189/202101/1535189-20210126182455451-1926330943.png)
```
whereis python3
```
![](https://img2020.cnblogs.com/blog/1535189/202012/1535189-20201225110258857-1147785979.png)

### 五、编辑python自启动
```
sudo vim /etc/crontab
```
![](https://img2020.cnblogs.com/blog/1535189/202012/1535189-20201225024612136-319055669.png)
```
crontab -e
```
crontab可能不能运行，因此在这里再次添加定时
![](https://img2020.cnblogs.com/blog/1535189/202012/1535189-20201225110424469-118105501.png)


### 六、修改my.sh的权限为777
```
cd 
sudo chmod -R 777 /root/my.sh
```

### 七、发送错误日志到邮箱
Centos7发错错误日志到邮箱：https://www.cnblogs.com/Lin1031/p/14401289.html#/c/subject/p/14401289.html
配置好环境之后，使用 empty.sh 脚本，在 shell 里设置自动启动的时间，如果之前的填报脚本出现错误日志，则会发送邮件。
注意：使用时，需要将 tiaobiao.py 最后一行输出注释掉。一般自动启动时间建议在设置自动填报时间之后的一小时。

### 八、批量填报
编写一个 sno.txt 文件，其内容为学号 省 市 区，使用 my.sh 脚本，进行批量读文件。
注意：sno.txt 中 学号为一行一个人，最后一行不能有空行。若使用批量填报，则定时则设置为该脚本。

### 九、无服务器使用（无脑，推荐）

### 使用 GitHub Actions（流程很简单 只要加个学号就行）

经过测试，大概在凌晨一点半的时候打卡成功

使用步骤:

- 点击右上角 `star` :)![image-20211023223415973](https://img2020.cnblogs.com/blog/1535189/202110/1535189-20211024011444420-1054435861.png)

- 克隆这个仓库到你名下

- ![image-20211023223437524](https://img2020.cnblogs.com/blog/1535189/202110/1535189-20211024011444220-574369804.png)

- 第一次使用需要确认

![屏幕截图 2021-10-24 012114](https://img2020.cnblogs.com/blog/1535189/202110/1535189-20211024012336869-1205037702.png)

![image-20211024012249533](https://img2020.cnblogs.com/blog/1535189/202110/1535189-20211024012336425-986933813.png)

- 在仓库设置里面, 设置 secrets 如下

  - `stuID`: 你的学号

    ![image-20211024004751004](https://img2020.cnblogs.com/blog/1535189/202110/1535189-20211024011443749-1912034824.png)

  - `API_KEY`: 你的通知[server酱](http://sc.ftqq.com/3.version)的api key，填写之后可以在程序完成打卡之后通知到微信，如果不填写不影响使用(类似的操作)
  -  `stuIDs`: 批量打卡的学号
 ![批量打卡](https://images.cnblogs.com/cnblogs_com/Lin1031/1924181/o_211128122132_%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20211128202040.png)


代码如果已经更改过的，需要保持代码的更新，同步即可

![image-20211024003508381](https://img2020.cnblogs.com/blog/1535189/202110/1535189-20211024011443314-1404804501.png)

### 参考资料
https://blog.csdn.net/chengxun02/article/details/105187996

https://blog.csdn.net/a12355556/article/details/112163669

https://github.com/IanSmith123/ucas-covid19
