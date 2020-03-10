# Vagrant Setup For Windows

# 环境要求
## 系统环境，权限和终端
windows10最新版系统，管理员权限，windows terminal。
## windows terminal的安装和设置
在Microsoft商店中下载（直接去github下载[https://github.com/microsoft/terminal/releases](https://github.com/microsoft/terminal/releases)）并安装windows terminal（preview）并更改颜色配置
![image.png](https://cdn.nlark.com/yuque/0/2020/png/731834/1582734470937-c41971a3-86ea-4714-af13-6f9e32875117.png#align=left&display=inline&height=165&name=image.png&originHeight=330&originWidth=1392&size=64300&status=done&style=none&width=696)
点击Settings
将设置的文本内容以以下代码覆盖
```

// To view the default settings, hold "alt" while clicking on the "Settings" button.
// For documentation on these settings, see: https://aka.ms/terminal-documentation

{
    "$schema": "https://aka.ms/terminal-profiles-schema",

    "defaultProfile": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",

    "profiles":
    {
        "defaults":
        {
             "colorscheme": "Solarized Dark"
        },
        "list":
        [
            {
                // Make changes here to the powershell.exe profile
                "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
                "name": "Windows PowerShell",
                "commandline": "powershell.exe",
                "hidden": false
            },
            {
                // Make changes here to the cmd.exe profile
                "guid": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",
                "name": "cmd",
                "commandline": "cmd.exe",
                "hidden": false
            },
            {
                "guid": "{b453ae62-4e3d-5e58-b989-0a998ec441b8}",
                "hidden": false,
                "name": "Azure Cloud Shell",
                "source": "Windows.Terminal.Azure"
            }
        ]
    },

    // Add custom color schemes to this array
        "schemes": [
        {
            "name": "Campbell",
            "foreground": "#F2F2F2",
            "background": "#0C0C0C",
            "colors": [
                "#0C0C0C",
                "#C50F1F",
                "#13A10E",
                "#C19C00",
                "#0037DA",
                "#881798",
                "#3A96DD",
                "#CCCCCC",
                "#767676",
                "#E74856",
                "#16C60C",
                "#F9F1A5",
                "#3B78FF",
                "#B4009E",
                "#61D6D6",
                "#F2F2F2"
            ]
        },
        {
            "name": "Solarized Dark",
            "foreground": "#FDF6E3",
            "background": "#073642",
            "colors": [
                "#073642",
                "#D30102",
                "#859900",
                "#B58900",
                "#268BD2",
                "#D33682",
                "#2AA198",
                "#EEE8D5",
                "#002B36",
                "#CB4B16",
                "#586E75",
                "#657B83",
                "#839496",
                "#6C71C4",
                "#93A1A1",
                "#FDF6E3"
            ]
        },
        {
            "name": "Solarized Light",
            "foreground": "#073642",
            "background": "#FDF6E3",
            "colors": [
                "#073642",
                "#D30102",
                "#859900",
                "#B58900",
                "#268BD2",
                "#D33682",
                "#2AA198",
                "#EEE8D5",
                "#002B36",
                "#CB4B16",
                "#586E75",
                "#657B83",
                "#839496",
                "#6C71C4",
                "#93A1A1",
                "#FDF6E3"
            ]
        },
        {
            "name": "Ubuntu",
            "foreground": "#EEEEEC",
            "background": "#2C001E",
            "colors": [
                "#EEEEEC",
                "#16C60C",
                "#729FCF",
                "#B58900",
                "#268BD2",
                "#D33682",
                "#2AA198",
                "#EEE8D5",
                "#002B36",
                "#CB4B16",
                "#586E75",
                "#657B83",
                "#839496",
                "#6C71C4",
                "#93A1A1",
                "#FDF6E3"
            ]
        },
        {
            "name": "UbuntuLegit",
            "foreground": "#EEEEEE",
            "background": "#2C001E",
            "colors": [
                "#4E9A06",
                "#CC0000",
                "#300A24",
                "#C4A000",
                "#3465A4",
                "#75507B",
                "#06989A",
                "#D3D7CF",
                "#555753",
                "#EF2929",
                "#8AE234",
                "#FCE94F",
                "#729FCF",
                "#AD7FA8",
                "#34E2E2",
                "#EEEEEE"
            ]
        }
    ],

    // Add any keybinding overrides to this array.
    // To unbind a default keybinding, set the command to "unbound"
    "keybindings": []
}

```

## 安装virtualbox和vagrant
安装virualbox：[https://www.virtualbox.org/](https://www.virtualbox.org/)
![image.png](https://cdn.nlark.com/yuque/0/2020/png/731834/1582733251676-67bce496-e1c5-423c-8209-dd0e34159c91.png#align=left&display=inline&height=304&name=image.png&originHeight=608&originWidth=813&size=128840&status=done&style=none&width=406.5)
选择windows hosts进行安装

安装vagrant：[https://www.vagrantup.com/downloads.html](https://www.vagrantup.com/downloads.html)
![image.png](https://cdn.nlark.com/yuque/0/2020/png/731834/1582733328193-220b69b1-dba2-4ce3-8e1e-c5474c079fba.png#align=left&display=inline&height=426&name=image.png&originHeight=851&originWidth=1211&size=96462&status=done&style=none&width=605.5)
# Vagrant使用
## 全栈box的添加并且vagrant up
查阅[https://github.com/ruilisi/quanzhan](https://github.com/ruilisi/quanzhan)下的readme
```shell
host $ git clone https://github.com/ruilisi/quanzhan.git
host $ cd quanzhan
host $ 找人要一个quanzhan.box,然后copy到quanzhan目录下面
host $ vagrant box add quanzhan.box --name quanzhan --force
host $ vagrant up
```
如果本地已有box，无需操作。

在vagrant up之后还未完成，需要Provision。

### 问题一：tmp文件夹缺失
```shell
VBoxManage.exe: error: Details: code E_FAIL (0x80004005), component ConsoleWrap, interface IConsole
Stderr: VBoxManage.exe: error: RawFile#0 failed to create the raw output file /tmp/ubuntu-bionic-18.04-cloudimg-console.log (VERR_PATH_NOT_FOUND)
```
解决方案：在C盘根目录下创建一个名为tmp的文件夹。

## 设置和使用网络专线
关与Chorme浏览器专用线路9119的使用方法：

- 下载插件SwitchOmega插件，新建情景，设置代理协议为HTTP，代理服务器为127.0.0.1，端口为9119

## Vagrant Provision
Route A

设置完专线之后

```bash
vagrant provision --provision-with pre

#接着联网更新，自动更新完成之后

vagrant reload

vagrant provision

vagrant ssh
```


### 可能问题
可能会遇到如下问题

- failed to lock apt for exclusive operation,

![image.png](https://cdn.nlark.com/yuque/0/2020/png/752281/1582791203143-5bb58e03-9b0f-47bc-b598-f959a3e14027.png#align=left&display=inline&height=92&name=image.png&originHeight=184&originWidth=750&size=87415&status=done&style=none&width=375)
解决方案：1.windows: 用管理员身份运行powershell或者cmd
2.mac: 在pre.yml 里面加become_user: root
                                become_method: sudo

- influxdb需要安装

通过官方下载[https://portal.influxdata.com/downloads/](https://portal.influxdata.com/downloads/)下载influxdb windows并安装

- PROXY env没有更新（gem.rubychina等等没有加到no-proxy里面）

解决方案：  vagrant plugin install vagrant-proxyconf

- kubectl无法下载（可能是网络问题）

C:\Users\hp\Projects\quanzhan\provisioning文件夹下roles.yml相关部分注释
```shell
    - andrewrothstein.kubectl
    - andrewrothstein.kubernetes-helm
    - ericsysmin.gcloud
```



## Git in Vagrant
### RouteA
vagrant ssh之后，检测git版本，git --version，为2.17.1。

正常干净的vagrant git环境
```shell
git config --global user.name "xxx"
git config --global user.email "xx@xx.com"

ssh-keygen

cat ~/.ssh/id_rsa.pub
#将出现的代码用ALT+C进行复制，ctrl+C会变成跳过。
```
出现git public key，去git官网，在设置中添加ssh key。

设置完成之后
```shell
ssh-add

ssh -T git@github.com

#出现Hi，xxx,成功
```

### RouteB
在使用git相关操作时如果遇到Permission denied可能是vagrant没有进行git配置。
![image.png](https://cdn.nlark.com/yuque/0/2020/png/731834/1582735054171-e6675b16-0a22-44a4-aecc-652fada63b44.png#align=left&display=inline&height=156&name=image.png&originHeight=234&originWidth=1118&size=192094&status=done&style=none&width=746)

需要先设置用户名和邮箱。此处的用户名为github的名称，邮箱为注册github的邮箱。
```shell
git config --global user.name "xxx"
git config --global user.email "xx@xx.com"
```
在C盘根目录./ssh目录下cp id_rsa* Projects/xxx/, mv id_rsa my_github, mv id_rsa.pub my_github.pub; 然后vagrant ssh，再mv ~/Projects/xxx/my_github* ~/.ssh/。vagrant的github就配置好了

然后在github上确认自己的settings中的sshkey是否和cat到的ssh key一致。

如果不一致则需要确认一下是否成功覆盖了vagrant中的my_github.pub文件。
