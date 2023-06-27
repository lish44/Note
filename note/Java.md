[hibernate](hibernate.md)

[java环境](java环境.md)

### 

加载服务配置
getInstrance();
    + 加载了sso 配置文件
    + 初始化了timer（）管理器
    + 初始化WsNetServer
        初始化 new HandshakeManager();
        初始化 new ConnCheckManager();
    + 设置了连接监听器？


initialize();
    + 用initialize 启动了三个线程
        + session管理 定时清理session
        + 清理过期连接
        + 用orm 查服务器列表，（第一次初始化了herbHibernate）然后把所有数据放到了serverlist key 是serverID            
        + 数据库定时清理过期


start
    + 进封好的WsNetServer去创建ws
    + 根据核心数创建监听线程启动了16个线程是在WebSocketServer:111

---

网络层接口 
`WebSocketAcceptor.class`
    + 通过override `open` `onClose` `onError` `onMessage` 等这些方法二次封装了网络层
    + 客户机每次连接 同过onOpen方法会定位到
        - WsNetServer.onWebsocketOpen()
            -   HandshakeManager.webSocketOpen() 每次连接都会新建一个会话

第一次握手发包在HandshakeManager.webSocketOpen().
二次握手在 Handshake.isSuccessed()

一次通讯的生命周期，第一次连接
    onOpen 会创建一个密钥 salt 返给client，client用salt加密后进行二次握手
    onMessage(WebSocket arg0, String arg1) arg1就是加密后的信息

interface
    fun1
    fun2

map < type, interface > dic
p = dic.get(type)
p.fun1

type是不同平台 
p是不同平台处理方式的对象，就是实现了interface 的一个类 ，这个类继承了interface，它代表了平台的处理方式，这样一个接口 抽象了 不同平台的处理


所有消息都通过WebSocketImpl.send(draft.createFrames(text, role == Role.CLIENT)); 发送的

```Csharp
using System;
using UnityEngine;
using System.Text;
using UnityWebSocket;
using Com.Game.Proto;
using Google.Protobuf;
using System.Security.Cryptography;

public class Network : MonoBehaviour
{
    private WebSocket ws;
    private string address = "ws://10.26.4.169:7700";

    private bool hasConnected = false;

    /// <summary>
    /// 发送登录信息
    /// </summary>
    public void SendLoginInfo()
    {
        var loginInfo = new UserLoginReq();
        loginInfo.Platform = "1";
        loginInfo.User = "2";
        loginInfo.Passwd = "3";
        loginInfo.Arg = "4";
        loginInfo.ServerId = 5;
        var data = loginInfo.ToByteArray();
        int protoLength = data.Length;
        int length = protoLength + 6;
        int cmd = 1;

        // 创建一个长度为length的byte数组
        var bytes = new byte[length];
        // 将protoLength转换为byte数组
        bytes[0] = (byte)(protoLength >> 24);
        bytes[1] = (byte)(protoLength >> 16);
        bytes[2] = (byte)(protoLength >> 8);
        bytes[3] = (byte)(protoLength);
        // 将01转换为byte数组
        bytes[4] = (byte)(cmd >> 8);
        bytes[5] = (byte)(cmd);
        // 将data转换为byte数组
        for (int i = 0; i < protoLength; i++)
        {
            bytes[i + 6] = data[i];
        }
        // 发送数据
        ws.SendAsync(bytes);
    }

    private void Start()
    {
        // 创建实例
        ws = new WebSocket(address);
        // 注册事件
        ws.OnOpen += OnOpen;
        ws.OnMessage += OnMessage;
        ws.OnClose += OnClose;
        ws.OnError += OnError;
        // 连接
        ws.ConnectAsync();
    }

    private void OnOpen(object sender, OpenEventArgs e)
    {
        Debug.Log("Connected");
    }

    private void OnMessage(object sender, MessageEventArgs e)
    {
        if (!hasConnected)
        {
            Debug.Log("Receive: " + e.Data);
            // 发送验证信息到服务器
            var str1 = e.Data.Replace("\0", ""); // 去除末尾的空字符，否则会导致字符串操作无效
            ws.SendAsync(Sha1Encrypt(str1, "^u7Y%GaNXGyZDs*3")); //发送数据
            hasConnected = true;
            return;
        }

        var bytes = e.RawData;
        int protoLength = (bytes[0] << 24) + (bytes[1] << 16) + (bytes[2] << 8) + bytes[3];
        var bytes2 = new byte[protoLength];
        for (int i = 0; i < protoLength; i++)
        {
            bytes2[i] = bytes[i + 6];
        }
        var userLoginRes = UserLoginRes.Parser.ParseFrom(bytes2);
        Debug.Log("Receive: " + userLoginRes);
    }

    private void OnClose(object sender, CloseEventArgs e)
    {
        Debug.Log("Disconnected");
    }

    private void OnError(object sender, ErrorEventArgs e)
    {
        Debug.Log("Error: " + e.Message);
    }

    /// <summary>
    /// SHA1 加密
    /// </summary>
    /// <param name="input">输入</param>
    /// <param name="key">key</param>
    /// <returns>加密后的字符串</returns>
    private string Sha1Encrypt(string input, string key)
    {
        // 将字符串和 key 连接起来，得到新的字符串 data
        string data = input + key;

        // 将字符串 data 转成字节数组
        byte[] bytes = Encoding.UTF8.GetBytes(data);

        // 创建 SHA1 实例
        SHA1 sha1 = SHA1.Create();

        // 计算哈希值
        byte[] hash = sha1.ComputeHash(bytes);

        // 将哈希值转成字符串返回
        return BitConverter.ToString(hash).Replace("-", "").ToLower();
    }
}


```



