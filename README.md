<center><div align="center">

<img src="https://avatars.githubusercontent.com/u/90495619?v=4" width="300" height="300" style="border-radius: 50%"></img>

<img alt="version" src="https://img.shields.io/github/last-commit/WAADRI/ChaoXing_node_signin.svg?style=for-the-badge&label=%E6%9C%80%E5%90%8E%E6%9B%B4%E6%96%B0&logo=velog&logoColor=BE95FF&color=7B68EE"/></img>
<img alt="stars" src="https://img.shields.io/github/stars/WAADRI/ChaoXing_node_signin.svg?style=for-the-badge&label=Stars&logo=undertale&logoColor=orange&color=orange"/></img>
<img alt="forks" src="https://img.shields.io/github/forks/WAADRI/ChaoXing_node_signin.svg?style=for-the-badge&label=Forks&logo=stackshare&logoColor=f92f60&color=f92f60"/></img>
<img alt="pr" src="https://img.shields.io/github/issues-pr-closed/WAADRI/ChaoXing_node_signin.svg?style=for-the-badge&label=PR&logo=addthis&logoColor=green&color=0AC18E"/></img>
<img alt="issues" src="https://img.shields.io/github/issues/WAADRI/ChaoXing_node_signin.svg?style=for-the-badge&label=Issues&logo=openbugbounty&logoColor=e38dff&color=e38dff"/></img>

</div></center>

<div align="center" style="font-weight:bold"><b>学习通在线自动签到系统签到节点接入脚本</b></div> 


用于自行部署可接入 [学习通在线自动签到系统](https://cx.waadri.top) 的签到节点，该节点脚本需配合主系统使用！

---


## 🎃 关于开源
由于~~怀疑被官方针对~~学习通频繁更新源码中的接口，为了确保所有功能可持续使用，此后将只发布最基础的签到代码，完整功能请登录自动签到系统使用官方节点进行体验


## ✨ 版本差异

|          |                                    exe版本                                    |                                    Python版                                     |                        Docker版                         |
| :------: | :---------------------------------------------------------------------------: | :-----------------------------------------------------------------------------: | :-----------------------------------------------------: |
| 适合人群 |                             有Windows电脑使用经历                             |                              有编程经验或Linux经验                              |                  有NAS经验或Linux经验                   |
| 功能差异 |                                       /                                       |                                        /                                        |                  仅支持 amd64 和 arm64                  |
| 下载链接 | [exe下载链接](https://api.waadri.top/ChaoXing/download/other-signin-node.exe) | [Python下载链接](https://api.waadri.top/ChaoXing/download/other-signin-node.py) | `ccr.ccs.tencentyun.com/misaka-public/waadri-sign-node` |

## 🎉 搭建教程

配置文件展示：

```yaml
# --- 邮件功能配置区 ---
email:
  # 用来发送邮件的邮箱，未填写则不发送邮件
  address: ''
  # 用来发送邮件的邮箱密码
  password: ''
  # 是否使用tls加密连接，默认为true
  use_tls: true
  # 邮件服务器的host主机名
  host: ''
  # 邮件服务器端口
  port: 465
  # 发件人名称
  user: ''
# --- 节点名称密码配置区 ---
node:
  # 节点名称，不能和已接入在线自动签到系统的其它自建节点名称重复
  name: ''
  # 节点密码，设置后用户需要在网站中输入正确的密码才能使用该节点，留空则为不设置密码，此时任何人均可使用该节点进行签到
  password: ''
# 是否启用debug模式，启用后日志输出更加详细，方便排查问题，建议使用时出现问题且命令行中未展示问题详细信息时再启用
debug: false
# 节点uuid，第一次使用时会随机生成，请勿更改
uuid: XXX
```

### 可执行版教程（exe版）

1. 双击运行，首次运行会在当前位置生成 `node_config.yaml` 配置文件。
2. 将 `node_config.yaml` 中的 `name` 修改为你喜欢的节点名称。
3. 再次双击运行。
4. 前往 [网站](https://cx.waadri.top) 选择你的节点使用。

### Python版教程
1. 安装好 `python3.10+` 环境

2. 安装依赖
```bash
pip install --user -r requirements.txt
```
3. 使用以下命令运行
```bash
curl -o "main.py" "https://api.waadri.top/ChaoXing/download/other-signin-node.py"
python3 main.py
```
4. 修改 `node_config.yaml` 配置文件的 `name` 为你喜欢的节点名称。
5. 再次运行。

### Docker版教程

#### 使用已构建的镜像

群友构建的镜像 `ccr.ccs.tencentyun.com/misaka-public/waadri-sign-node`（仅支持 `amd64` 和 `arm64`）

镜像使用 Github Action 构建，详见 [构建脚本](https://github.com/Misaka-1314/SignNode-AutoBuild)

将配置文件目录下运行，首次运行会生成 `node_config.yaml` 配置文件。

```bash
docker run -d \
    --name=sign-node \
    -v $(pwd):/data \
    --restart=always \
    --dns=223.5.5.5 --dns=114.114.114.114 \
    ccr.ccs.tencentyun.com/misaka-public/waadri-sign-node
```

#### 自己构建镜像

1. 构建镜像
```bash
curl -o "main.py" "https://api.waadri.top/ChaoXing/download/other-signin-node.py"
docker build -t your_image_name .
```


2. 运行
```bash
docker run -d \
    --name=sign-node \
    -v $(pwd):/data \
    --restart=always \
    --dns=223.5.5.5 --dns=114.114.114.114 \
    your_image_name
```

## 🎉 使用

运行上线后可在在线自动签到系统中点击 **其它第三方自选节点**，会自动弹出自选节点列表，选择并输入你设置的密码后即可使用所选节点进行签到监控。

![image](https://github.com/WAADRI/ChaoXing_node_signin/assets/90495619/3f48708a-8e71-4147-8005-c4a266782014)

### 🎃 注意事项
- 仅供学习交流，不要用于非法用途
- 为防止部分接口被恶意利用，第三方节点不支持手动签到模式，不支持开启签到监控状态下自动更新用户签到信息（签到过程中仍可在网站上修改签到信息但不会自动同步至第三方节点服务端）。为防止官方更新导致功能失效，第三方节点不再支持反钓鱼签到模式和签到信息盗用模式，不再支持使用接口4进行签到监控。除此以外第三方节点不支持节点离线后自动更换签到节点，且无7无签到自动停止签到监控的限制
- 以上限制为第三方签到节点的限制，此番举措为防止官方更新导致功能失效，若要体验最完整的功能还请使用官方节点进行签到监控
- 节点脚本不要搭建在云服务器厂商的IP环境下，否则可能会被学习通官方封禁IP地址导致无法进行签到监控，请在四大运营商或教育网的网络环境下搭建
- 如有侵权请联系我们删除：[Email](mailto:WiFi86@qq.com)