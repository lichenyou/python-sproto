一：
# sproto dump
parse sproto file `.sproto` to binary file `.spb` , c# code `.cs` or go code `.go`.

usage is as follows:
```
usage: lua sprotodump.lua <option> <sproto_file1 sproto_file2 ...> [[<out_option> <outfile>] ...] [namespace_option]

    option: 
        -cs              dump to cSharp code file
        -spb             dump to binary spb  file
        -go              dump to go code file
        -md              dump to markdown file
        
    out_option:
        -d <dircetory>               dump to speciffic dircetory
        -o <file>                    dump to speciffic file
        -p <package name>            set package name(only cSharp code use)

    namespace_option:
        -namespace       add namespace to type and protocol
```

二：
pip install setup.py 安装python的sproto

from sproto import SprotoRpc
import pysproto
from pysproto import sproto_create, sproto_type, sproto_encode, sproto_decode, sproto_pack, sproto_unpack, sproto_protocol, sproto_dump, sproto_name

1、创建解析类型
          with open("pingtai.spb", "r") as fh:
            content = fh.read()
        sproto_obj = SprotoRpc(content, content, "package")

2、发送request请求
    source = {
                "inviteCode" : "",
                "loginDevice" : 1,
                "loginMacCode" : self.loginMacCode,
                "loginSrc" : 1,
                "nickname" :"",
                "openId" : "",
                "password" : self.password,
                "unionId" : "",
                "username" : self.username
            }
            p = sproto_obj.request('login', source, 1)
            self.sockets.send(struct.pack(">H"+str(len(p))+"s",len(p),p))

3、解析response（【2:】表示前两个字节为data长度，不需要解析）
    responseData = sproto_obj.dispatch(data[2:])
        
