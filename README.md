[toc]
## TortoiseGit 仓库管理


#### 生成ppk格式私钥

在安装过TortoiseGit的机器上应该都会有一个PuTTYGen的工具
<div align="left">
  <img src="images/puttygen00.png" alt="Editor" width="300">
</div>

打开后不要点Generate，而是点Load，加载之前生成的私钥：
<div align="left">
  <img src="images/puttygen01.png" alt="Editor" width="300">
</div>

打开加载对话框时，选中右下角"All Files"，再选择之前生成并下载到Windows机器的id_rsa。
<div align="left">
  <img src="images/puttygen02.png" alt="Editor" width="300">
</div>

加载私钥后如果顺利就该弹出对话框告诉你一切成功，点确定关闭对话框。
<div align="left">
  <img src="images/puttygen03.png" alt="Editor" width="300">
</div>

点"Save private key"，保存为ppk文件
<div align="left">
  <img src="images/puttygen04.png" alt="Editor" width="300">
</div>

此时会弹出告警，说是否保存未受密码保护的密钥，为了避免今后每用一次都需要输密码，这里就直接点是。

当然，如果你实在没有安全感，或者是受虐狂体质，也可以点否，然后在主界面的"Key passphrase"中输入密码再重新保存。
<div align="left">
  <img src="images/puttygen05.png" alt="Editor" width="300">
</div>

在后续窗口中选择一个目录，输入一个文件名，然后确定，即可生成ppk格式的私钥，到这时可以把PuTTYGen关掉了。

这里请 **一定一定一定** 记住你保存的位置和文件名，否则下次用的时候找不到，你还得再来一遍。
<div align="left">
  <img src="images/puttygen06.png" alt="Editor" width="300">
</div>

#### 添加公钥到GitLab

打开GitLab并以自己的帐户登录，按下图数字1,2,3顺序点击，找到添加ssh key的地方，并在4号框中粘贴进之前生成的id_rsa.pub文件的内容，看下示例中的格式，别找错文件，再点按钮5："Add key"，即完成添加。

其中的标题用于区分不同的ssh-key，只要不与已有的相同即可，不用太在意。

![gitlab00](images/gitlab00.png)

#### TortoiseGit中使用私钥

在TortoiseGit目录中找到Pageant，如下图：
<div align="left">
  <img src="images/pageant00.png" alt="Editor" width="300">
</div>

点击运行后好像不会出现界面，可以在任务栏托盘中找到它：
<div align="left">
  <img src="images/pageant01.png" alt="Editor" width="300">
</div>

右击任务栏托盘中Pageant的图标，并在弹出菜单中选择"Add Key"
<div align="left">
  <img src="images/pageant02.png" alt="Editor" width="300">
</div>

在弹出的文件选择对话框中选择之前生成的ppk私钥，之前说 **一定** 记住ppk私钥的文件名和位置，应该没这么快忘吧。

也可以在Pageant右键菜单中选"View Keys"，查看确认你的私钥添加成功：
<div align="left">
  <img src="images/pageant04.png" alt="Editor" width="300">
</div>

注意：Pageant工具好像没办法自动加载ppk私钥，也就是说每次电脑启动后如果要用TortoiseGit都得手工加载私钥这么一次。谁如果知道怎么样自动加载，记得告诉我让我知道。

#### 测试验证

登录GitLab，并打开任意一个工程，找到URL并选择复制，注意，这里要SSH形式的URL，而非HTTP形式的。
<div align="left">
  <img src="images/gitlab01.png" alt="Editor" width="300">
</div>

在文件管理器中，选个目录在空白处点右键选Git Clone...
<div align="left">
  <img src="images/git00.png" alt="Editor" width="300">
</div>

在弹出对话框的URL中粘贴入刚复制的URL，并确定。

小提示，这里一般都会自动填入在剪贴板中的内容，如果你复制了URL再打开Git Clone，就省了粘贴这一步了。
<div align="left">
  <img src="images/git01.png" alt="Editor" width="300">
</div>

如果TortoiseGit成功将远程库克隆到本地，则ppk私钥已成功生效。
<div align="left">
  <img src="images/git02.png" alt="Editor" width="300">
</div>

**至此，TortoiseGit和PyCharm/IDEA/WebStorm等IDE工具均已可直接使用GIT不再会提示密码。**

TortoiseGit 使用 pageant 密钥助手实在是太麻烦了，使用时经常会忘记打开，有没别的方法，比如直接使用 .ssh 目录下的 id_rsa 密钥？

答案是：有的。

打开命令行，输入 ssh，看是否有这个命令。

如果是有这样的显示，则说明是安装过 ssh 命令的，可以直接用。
<div align="left">
  <img src="images/ssh_cmd.png" alt="Editor" width="400">
</div>

如果是提示“'ssh' 不是内部或外部命令，也不是可运行的程序或批处理文件。"，则说明没有安装。

需要按下述方法先安装上：

先用鼠标在开始菜单上右击，然后选择“应用和功能”。
<div align="left">
  <img src="images/install_ssh_1.png" alt="Editor" width="400">
</div>

再点击应用和功能对话框的“可选功能”。
<div align="left">
  <img src="images/install_ssh_2.png" alt="Editor" width="400">
</div>

点击“添加功能”。
<div align="left">
  <img src="images/install_ssh_3.png" alt="Editor" width="400">
</div>

在搜索框输入"OpenSSH"，并选择OpenSSH 客户端，然后点击安装按钮。
<div align="left">
  <img src="images/install_ssh_4.png" alt="Editor" width="400">
</div>

有此显示说明安装完成。
<div align="left">
  <img src="images/install_ssh_5.png" alt="Editor" width="400">
</div>

然后，再打开命令行窗口，确认ssh命令已经安装成功。
<div align="left">
  <img src="images/ssh_cmd.png" alt="Editor" width="400">
</div>

在任意目录右键，并选择TortoiseGit -> 设置
<div align="left">
  <img src="images/config_tortoise_1.png" alt="Editor" width="400">
</div>

在网络-> SSH 客户端中，点击选择按钮。
<div align="left">
  <img src="images/config_tortoise_2.png" alt="Editor" width="400">
</div>

在C:\Windows\System32\OpenSSH目录，选中ssh.exe命令，并点击打开。
<div align="left">
  <img src="images/config_tortoise_3.png" alt="Editor" width="400">
</div>

确保TortoiseGit 网络设置中的SSH客户端指向刚刚所选的ssh命令。
<div align="left">
  <img src="images/config_tortoise_4.png" alt="Editor" width="400">
</div>

点击确定设置完成后，关闭以前用的Pageant，然后尝试去pull 任意的Git仓库，看看是否生效吧。

**强烈推荐福利！！！每天免费领取饿了么，美团外卖红包（买菜，点美食都可以）**

<div align="left">
  <img src="https://user-images.githubusercontent.com/21699695/221159459-81384c4b-67a0-4616-b885-515965989fa4.png" alt="Editor" width="600">
</div>
