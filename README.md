# Propagation

Because of the slow download speed from Apple servers, Chinese iOS developers would download Xcode from third party websites, such as Baidu Yun (now called Baidu WangPan), a cloud storage service hosted by Baidu, or get copies from co-workers. Attackers took advantage of this situation by distributing compromised versions on such file hosting websites.

The attacker used a compiler backdoor attack. The novelty of this attack is the modification of the Xcode compiler. However, according to documents leaked by Edward Snowden, CIA security researchers from Sandia National Laboratories claimed that they "had created a modified version of Apple’s proprietary software development tool, Xcode, which could sneak surveillance backdoors into any apps or programs created using the tool."[18]

# Modified files

Known versions of XcodeGhost add extra files[13] to the original Xcode application:

Core service framework on iOS, iOS simulator and OS X platforms
IDEBundleInjection framework added on iOS, iOS simulator and OS X platforms
XcodeGhost also modified the linker to link the malicious files[16] into the compiled app. This step is reported on the compiling log but not on the Xcode IDE.

Both iOS and OS X apps are vulnerable to XcodeGhost.

# Deployment

XcodeGhost compromised the CoreServices layer, which contains highly used features and frameworks used by the app.[19] When a developer compiles their application with a compromised version of Xcode, the malicious CoreServices are automatically integrated into the app without the developer's knowledge.

Then the malicious files will add extra code in UIWindow class and UIDevice class. The UIWindow class is "an object that manages and coordinates the views an app displays on a device screen".[20]

The UIDevice class provides a singleton instance representing the current device. From this instance the attacker can obtain information about the device such as assigned name, device model, and operating-system name and version.[



# Remote control security risks

XcodeGhost can be remotely controlled via commands sent by an attacker from a Command and control server through HTTP. This data is encrypted using the DES algorithm in ECB mode. Not only is this encryption mode known to be weak, the encryption keys can also be found using reverse engineering. An attacker could perform a man in the middle attack and transmit fake HTTP traffic to the device (to open a dialog box or open specific app for example).

# Stealing user device information

When the infected app is launched, either by using an iPhone or the simulator inside Xcode, XcodeGhost will automatically collect device information such as:

Current time
Current infected app's name
The app's bundle identifier
Current device's name and type
Current system's language and country
Current device's UUID
Network type
Then the malware will encrypt those data and send it to a command and control server. The server differs from version to version of XcodeGhost; Palo Alto Networks was able to find three server URLs:

http://init.crash-analytics.com
http://init.icloud-diagnostics.com
http://init.icloud-analysis.com
The last domain was also used in the iOS malware KeyRaider

# Read and write from clipboard



XcodeGhost is also able, each time an infected app is launched, to store the data written in the iOS clipboard. The malware is also able to modify this data. This can be particularly dangerous if the user uses a password management app.

# Hijack opening specific URLs



XcodeGhost is also able to open specific URLs when the infected app is launched. Since Apple iOS and OS X work with Inter-App Communication URL mechanism[22] (e.g. 'whatsapp://', 'Facebook://', 'iTunes://'), the attacker can open any apps installed on the compromised phone or computer, in the case of an infected macOS application. Such mechanism could be harmful with password management apps or even on phishing websites.

# Prompting alert dialog



In its current known version XcodeGhost cannot prompt alert dialogs on the user device.[16] However, it only requires minor changes.

By using a UIAlertView class with the UIAlertViewStyleLoginAndPasswordInput property, the infected app can display a fake alert dialog box that looks like a normal Apple ID user credential check and send the input to the Command and control server.

# XcodeGhost
"XcodeGhost" Source
关于所谓”XcodeGhost”的澄清

首先，我为XcodeGhost事件给大家带来的困惑致歉。XcodeGhost源于我自己的实验，没有任何威胁性行为，详情见源代码:https://github.com/XcodeGhostSource/XcodeGhost

所谓的XcodeGhost实际是苦逼iOS开发者的一次意外发现：修改Xcode编译配置文本可以加载指定的代码文件，于是我写下上述附件中的代码去尝试，并上传到自己的网盘中。

在代码中获取的全部数据实际为基本的app信息：应用名、应用版本号、系统版本号、语言、国家名、开发者符号、app安装时间、设备名称、设备类型。除此之外，没有获取任何其他数据。需要郑重说明的是：出于私心，我在代码加入了广告功能，希望将来可以推广自己的应用（有心人可以比对附件源代码做校验）。但实际上，从开始到最终关闭服务器，我并未使用过广告功能。而在10天前，我已主动关闭服务器，并删除所有数据，更不会对任何人有任何影响。

愿谣言止于真相，所谓的"XcodeGhost"，以前是一次错误的实验，以后只是彻底死亡的代码而已。

需要强调的是，XcodeGhost不会影响任何App的使用，更不会获取隐私数据，仅仅是一段已经死亡的代码。

再次真诚的致歉，愿大家周末愉快
