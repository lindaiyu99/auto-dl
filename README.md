# auto-download

qbittorrent 自动刷下载量，并且数据**不**真实写入硬盘。

据测试，用于刷下载量的种子大小与机器内存没有依赖关系。


需要安装 [httpie](https://httpie.org/)。改成 curl 也可以，懒……


## 使用

1. 配置好 `config.sh` 后，第一次需要手动运行以便创建`空设备`(直接运行 config.sh 即可)。

如果有必要，刷完后记得删掉创建的空设备文件。

torrent 内容必须是当个文件！ (否则每一个文件你都需要自己创建对应的`空设备文件`)

2. 添加命令`/path/of/auto-dl/run.sh  "%N"`到qbittorrent `Torrent 完成时运行外部程序`处。

3. 可以添加`crontab`任务，以便及时将下载量汇报给tracker计入统计。比如：
```sh
# 不建议太快
*/6 *  * * * /path/of/auto-dl/run.sh >/dev/null 2>&1
```
## 其他

同一个种子下载完成后重新下载可能需要等待 20分钟甚至更久，因此推荐使用大体积的 原盘 ISO 文件刷。

因为不用预先分配磁盘，以及写入硬盘，下载速度几乎只与网络情况有关。一般挂后台几天刷个几百G还是很轻松的。

如果需要短时间大量刷下载量，可以做一个 list __(细水长流，别太猛了)__，减小 tracker 反应迟钝带来的影响。

## License

GPL-3

