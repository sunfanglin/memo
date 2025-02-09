# Tips
在星逸集群上编译时遇到 找不到 .mod 文件的错误，最后提示编译出错，生成的real.exe无法运行，这时候
连续运行两遍编译命令，则成功。

此问题在WPS上也存在，不能编译出ungrib.exe
此时也是运行两遍编译命令

注意，不要运行 ./clean -a 命令

## 记录
S 小网格 151
L 大网格 178

1p8_L  step=10 fail
1p8_L  step=8 OK
1p7_S  step=1 OK
1p7_S  step=2 fail
1p6_L  step=1 fail



> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0MDY1NTY0NTVdfQ==
-->