# IFS替代空格

![image](https://user-images.githubusercontent.com/52622597/210207396-1cdc8a0e-c2ee-4126-b66d-d88008baae15.png)

如果题目将空格给删除了，则可以使用${IFS}代替空格

![image](https://user-images.githubusercontent.com/52622597/210207484-838e32ee-04d3-4149-b156-29dacc50e150.png)

# python逃逸

https://book.hacktricks.xyz/generic-methodologies-and-resources/python/bypass-python-sandboxes

或者使用这个脚本来绕过
```
#!/usr/bin/env python3

import argparse
import os
import sys

# Ensure that this includes an argument for the file
parser = argparse.ArgumentParser()
parser.add_argument("script", type=str)
args = parser.parse_args()

if not os.path.exists(args.script):
        sys.stderr.write(f"'{args.script}' not a file")

with open(args.script, "rb") as h:
        contents = h.read().decode('utf-8')

code_string = "+".join([f"chr({ord(x)})" for x in contents])
code_string = f"{code_string}"

script_string = "+".join([f"chr({ord(x)})" for x in "<script>"])
script_string = f"{script_string}"

exec_string = "+".join([f"chr({ord(x)})" for x in "exec"])
exec_string = f"{exec_string}"

print(f'python -c "exec(compile({code_string}, {script_string}, {exec_string}))"')
```

![image](https://user-images.githubusercontent.com/52622597/210207901-468b234f-987e-4567-a8f9-96888d0e5c91.png)


# /etc/passwd绕过登录

如果拥有可以修改/etc/passwd文件权限的话，可以将x删除

![image](https://user-images.githubusercontent.com/52622597/210208043-61053f6c-f048-4ec4-bed6-9cc4739a5c49.png)

x代表的是此用户是否需要用密码登录

![image](https://user-images.githubusercontent.com/52622597/210208086-66567b60-b700-4ba8-a203-ae24af937288.png)


# 使用cat命令从剪贴板导入字符串
如果目标机子没有vim或者vi或者nano等文本编辑器，则可以使用cat命令覆盖文本

首先需要将要输入的字符复制一下
然后在目标机子上输入
```
cat<<EOF > /etc/passwd
```
然后ctrl+v粘贴内容

![image](https://user-images.githubusercontent.com/52622597/210208322-525bf055-141d-4550-b148-2396c88729a2.png)

最后输入EOF退出

![image](https://user-images.githubusercontent.com/52622597/210208403-9e705565-44cf-4116-b2e9-75fa2cb42fc6.png)

![image](https://user-images.githubusercontent.com/52622597/210208439-40bfb762-193d-4ecd-96db-6060bfbc0a5a.png)


