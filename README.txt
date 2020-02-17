主要是一些 YouTube 下载下来的视频.

如果视频超过 100M, github 是不允许上传的,我的方法是使用 split 命令

split BigFile.mp4 -b 40M -d -a 1 SmallFile.mp4
    -b --bytes=SIZE         指定按多少个字节进行拆分,后面可以跟 K, M, G
    -a <后缀长度>           默认的后缀长度为2
    -d                      使用数字作为后缀
    -<行数> 或 -l <行数>    指定每多少行进要拆分一个文件
    -C --line-bytes=SIZE    每一输出行归档中,单行的最大 bytes 数

split -b 10K data.file
split -b 10K data.file -d
split -b 10M data.file -d -a 2
split -l 10 data.file


split 会把源文拆分成指定大小的多个小文件,如果要合成原来的文件,如下
假设有两个小文件是 SmallFile.mp41 SmallFile.mp42
只需如下
    cat SmallFile.mp42 >> SmallFile.mp41
        # 注意一定是要追加重定向
    mv SmallFile.mp41 SmallFile.mp4
        # 最后的这个 SmallFile.mp4 就是源文件
    同理,3个或3个以上文件
        SmallFile.mp43 >> SmallFile.mp42
        SmallFile.mp42 >> SmallFile.mp41
        mv SmallFile.mp41 SmallFile.mp4
