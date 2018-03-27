# 使用Git抓取有变动的csv条目
1. 将下载得到的原始CSV另存为UTF-8+BOM

2. 使用excel另存为新的CSV, 用来删除单行中非必须的引号并更新换行符(翻译后另存的csv均无此类引号), 否则git中存在冗余diff项

3. 修正过的csv上传git, 存master树

4. 将翻译过的csv用同样名字上传并存到新的树(编号+汉化者)

5. 用git gui查询历史得到diff, 全选复制

6. 新建空文本粘贴, 以正则进行全局替换后复制
-	^@@.*\r\n	*去掉省略行标记*
-	^ \d+.*\r\n	*去掉diff行上下显示的符合行*
-	^-.*\r\n	*去掉旧diff行*
-	^\+		*去掉新diff行开头的+号*

7. 新建csv, 第一行为id,text,sound,timestamp,translate, 粘贴所有diff行, 另存为UTF-8无BOM

8. import, 进入队列的门槛是10000字节, 需要即时显示时需要拆分
