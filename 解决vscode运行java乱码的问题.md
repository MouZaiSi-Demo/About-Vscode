默认情况下，Windows上的VSC运行Java经常会出现乱码。网上大部分解决方法都是错误的，那些作者往往不具备足够的知识。我虽然没学多少Java，但对使用VSC还是有一些经验的。

### 结论
- 源文件使用UTF8编码
- 路径中不能有中文
- 若使用`Code Runner："code-runner.runInTerminal": true`、`code-runner.executorMap`中的`java`，`javac`后添加`-encoding utf-8`
- 若要debug，launch.json中添加`"encoding": "GBK"`。搜索修改`launcher.bat`，删掉`chcp.com 65001 > NUL`这一句，保存。 此文件在我的电脑上的路径在`C:\Users\<用户名>\.vscode\extensions\vscjava.vscode-java-debug-0.34.0\scripts`，且`java-debug`扩展更新后有需要再修改。也许他们未来会修复
- 确保没有启用“Beta版：使用Unicode UTF-8提供全球语言支持”。默认情况下是没有启用的
- 确保没有设置`-Dfile.encoding=UTF-8`

### 说明
- UTF8是现代化的编码，当然优先选择
- Code Runner默认在“输出”面板中运行，无法输入内容，肯定要不得
- javac和java命令行在不指定编码时默认都和系统编码一致，即GBK。但是我们的源文件用的是UTF8，所以需要指定javac的encoding参数
- 系统编码设置为UTF8时会使得程序无法读取输入，这是不可接受的。我认为这是Windows的BUG。我测试的几种语言只有Python能读取。所以不能启用那个控制面板的选项，也不能使用chcp 65001。系统编码一定只能是默认的936(GBK)
- launch.json的encoding的默认值是UTF8，此项影响的就是`-Dfile.encoding`，需要改成系统编码即GBK。编译用的是VSC的`files.encoding`设置，默认是UTF8，无需更改
---
### 转载说明:

作者：谭九鼎
链接：https://zhuanlan.zhihu.com/p/380930006
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。