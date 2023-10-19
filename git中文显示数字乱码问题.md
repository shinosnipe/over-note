# git中文显示数字乱码问题

修改git的全局配置即可，如下：

```sh
git config --global core.quotepath false
git config --global gui.encoding utf-8
git config --global i18n.commitencoding utf-8
git config --global i18n.logoutputencoding utf-8
```
