# linux设置相关

## Ubuntu

### ubuntu中文语言环境

在docker里使用ubuntu设置中文locale时可能会不存在`/etc/locale.gen`，需要安装字符集：

```sh
apt install language-pack-zh-hans
```