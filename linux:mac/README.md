# gojump SSH远程服务跳板
    可以通过gojump选择服务器地址，进行SSH远程访问

## 使用

1. 配置SSH服务
```
cat << EOF > ~/.gojump
#test env
test=0.0.0.0 22 descrition password
EOF
```
2. 调用 gojump

```
> gojump test
> 1 0.0.0.0 descrition
> 请选择:

# 选择1，则SSH远程到服务器

```