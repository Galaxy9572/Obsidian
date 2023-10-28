> 标签： #Mac #TimeMachine 

> 参考： [如何更好地清理 Time Machine 备份 - 少数派](https://sspai.com/post/59368#!)

# tmutil 命令行工具

macOS 自带 `tmutil` 工具，能够实现查看备份、创建备份、删除备份、比较备份等功能。

其中，`tmutil listbackups` 命令可以显示 Time Machine 中的所有备份：

```
$ tmutil listbackups
/Volumes/时间机器备份/Backups.backupdb/blanboom-studio/2019-12-21-200941
/Volumes/时间机器备份/Backups.backupdb/blanboom-studio/2020-01-05-221538
/Volumes/时间机器备份/Backups.backupdb/blanboom-studio/2020-01-19-203155
```

`tmutil delete` 命令则可以删除 Time Machine 中的指定备份：

```
$ sudo tmutil delete /Volumes/时间机器备份/Backups.backupdb/blanboom-studio/2019-02-01-211852 
Deleting: /Volumes/时间机器备份/Backups.backupdb/blanboom-studio/2019-02-01-211852
Deleted (427.2M): /Volumes/时间机器备份/Backups.backupdb/blanboom-studio/2019-02-01-211852
```

有了这两条命令，可以方便地在 shell 脚本中使用，进行批量删除备份的操作。