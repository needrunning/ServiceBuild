>共存，切换，兼容
>
系统中涉及到服务商对接模块的，设计之初必须考虑多服务商的共存，切换，兼容。
这里的服务商包括 推送系统的推送服务商，极光，信鸽，sms短信服务商，开票业务服务商，呼叫中心服务商等。这类服务商提供的服务，可以理解为SAAS服务。
### 解决方案稳定吗？
第三方服务商提供的都是某个领域的解决方案，是否稳定可靠，在对接之初是一个未知数，只有生产环境运行之后才有答案，这也是为什么要在设计之初就考虑切换，共存的另一个原因

要实现共存，切换和兼容有几个问题需要考虑

### 业务字段兼容

现在行业服务商对接都是服务接口方面的对接，json数据结构，http协议这些是行业共识了。索然协议有共识，但是实现细节各式各样，每个供应商对于接口的实现不同，同一业务含义的字段表示不同，遇到这一问题如何解决？

>分清对接方和服务方

解决这一问题的核心切入点是以哪个系统为主。这里的系统包括对接方业务系统和服务方开放系统两类。

优先推荐以业务系统字段描述为主，在对接开发时做字段映射来实现。

实现以自我业务系统为主的设计之后，可以进而实现切换和多服务商共存。

-----------------------------------

文章已同步到公众号《图南科技》欢迎关注

![图南科技.png](https://upload-images.jianshu.io/upload_images/5651-f9a95406471f320b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)