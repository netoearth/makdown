![](https://tonybai.com/wp-content/uploads/an-intro-of-govulncheck-1.png)

[本文永久链接](https://tonybai.com/2022/09/10/an-intro-of-govulncheck) – https://tonybai.com/2022/09/10/an-intro-of-govulncheck

___

2022年9月7日，Go安全团队在Go官博发表文章[《Vulnerability Management for Go》](https://go.dev/blog/vuln)，正式向所有Gopher介绍Go对安全漏洞管理的工具和方案。

在这篇文章中，Go安全团队引入了一个名为[govulncheck](https://github.com/golang/vuln/tree/master/cmd/govulncheck)的命令行工具。这个工具本质上只是[Go安全漏洞数据库(Go vulnerability database)](https://vuln.go.dev/)的一个**前端**，它通过[Go官方维护的vuln仓库](https://github.com/golang/vuln)下面的[vulncheck包](https://github.com/golang/vuln/tree/master/vulncheck)对你仓库中的Go源码或编译后的Go应用可执行二进制文件进行扫描，形成源码的调用图(callgraph)和调用栈(callstack)。

vuln仓库下面的client包则提供了访问漏洞数据源(支持多数据源)的接口和默认实现，开发人员可以基于module的路径或ID从漏洞数据库中查找是否存在已知的漏洞。而漏洞项采用[OSV, Open Source Vulnerability format](https://ossf.github.io/osv-schema/)格式存储和传输，vuln仓库同样提供了对osv格式的实现[包osv](https://github.com/golang/vuln/tree/master/osv)。

![](https://tonybai.com/wp-content/uploads/an-intro-of-govulncheck-2.png)  

图：Go安全漏洞方案架构 – 来自Go官方博客

> 注：你也可以基于vuln仓库下面的vulncheck包、client包等开发你自己的vulnerability检查前端，或将其集成到你的组织内部的工具链中。

和sumdb、proxy等一样，Go官方维护了一个默认的漏洞数据库vuln.go.dev，如上图所示，该数据库接纳来自知名漏洞数据源的数据，比如：[NVD](https://nvd.nist.gov/)、[GHSA](https://www.cdc.gov/globalhealth/security/what-is-ghsa.htm)等，Go安全团队发现和修复的漏洞以及最广大的go开源项目维护者提交的漏洞。

如果你是知名go开源项目的维护者，当你发现并修复你的项目的漏洞后，可以在[Go漏洞管理页面](https://go.dev/security/vuln/)找到不同类型漏洞的提交/上报入口，Go安全团队会对你上报的公共漏洞信息进行审核和确认。

好了，作为Gopher，我们更关心的是我们正在开发的Go项目中是否存在安全漏洞，这些漏洞或是来自Go编译器，或是来自依赖的有漏洞的第三方包。我们要学会使用govulncheck工具对我们的项目进行扫描。

govulncheck目前维护在golang.org/x/vuln下面，按照官博的说法，后期该工具会随同Go安装包一并发布，但是否会集成到go命令中尚不可知。现在要使用govulncheck，我们必须手动安装，命令如下：

```
$go install golang.org/x/vuln/cmd/govulncheck@latest
```

安装成功后，便可以在你的Go项目根目录下执行下面命令对整个项目进行漏洞检查了：

```
$govulncheck ./...
```

下面是我对自己项目的扫描的结果(扫描时使用的是Go 1.18版本)：

```
$govulncheck ./...
govulncheck is an experimental tool. Share feedback at https://go.dev/s/govulncheck-feedback.

Scanning for dependencies with known vulnerabilities...
Found 9 known vulnerabilities.

Vulnerability #1: GO-2022-0524
  Calling Reader.Read on an archive containing a large number of
  concatenated 0-length compressed files can cause a panic due to
  stack exhaustion.

  Call stacks in your code:
      raft/fsm.go:193:29: example.com/go/mynamespace/demo1/raft.updOnlyLinearizableSM.RecoverFromSnapshot calls io/ioutil.ReadAll, which eventually calls compress/gzip.Reader.Read

  Found in: compress/gzip@go1.18
  Fixed in: compress/gzip@go1.18.4
  More info: https://pkg.go.dev/vuln/GO-2022-0524

Vulnerability #2: GO-2022-0531
  An attacker can correlate a resumed TLS session with a previous
  connection. Session tickets generated by crypto/tls do not
  contain a randomly generated ticket_age_add, which allows an
  attacker that can observe TLS handshakes to correlate successive
  connections by comparing ticket ages during session resumption.

  Call stacks in your code:
      raft/raft.go:68:35: example.com/go/mynamespace/demo1/raft.NewRaftNode calls github.com/lni/dragonboat/v3.NewNodeHost, which eventually calls crypto/tls.Conn.Handshake

  Found in: crypto/tls@go1.18
  Fixed in: crypto/tls@go1.18.3
  More info: https://pkg.go.dev/vuln/GO-2022-0531

... ...

Vulnerability #6: GO-2021-0057
  Due to improper bounds checking, maliciously crafted JSON
  objects can cause an out-of-bounds panic. If parsing user input,
  this may be used as a denial of service vector.

  Call stacks in your code:
      cmd/demo1/main.go:352:23: example.com/go/mynamespace/demo1/cmd/demo1.main calls example.com/go/mynamespace/common/naming.Register, which eventually calls github.com/buger/jsonparser.GetInt

  Found in: github.com/buger/jsonparser@v0.0.0-20181115193947-bf1c66bbce23
  Fixed in: github.com/buger/jsonparser@v1.1.1
  More info: https://pkg.go.dev/vuln/GO-2021-0057

... ...
Vulnerability #9: GO-2022-0522
  Calling Glob on a path which contains a large number of path
  separators can cause a panic due to stack exhaustion.

  Call stacks in your code:
      service/service.go:45:12: example.com/go/mynamespace/demo1/service.NewPubsubService calls example.com/go/mynamespace/common/log.Logger.Fatal, which eventually calls path/filepath.Glob

  Found in: path/filepath@go1.18
  Fixed in: path/filepath@go1.18.4
  More info: https://pkg.go.dev/vuln/GO-2022-0522

=== Informational ===

The vulnerabilities below are in packages that you import, but your code
doesn't appear to call any vulnerable functions. You may not need to take any
action. See https://pkg.go.dev/golang.org/x/vuln/cmd/govulncheck
for details.

Vulnerability #1: GO-2022-0537
  Decoding big.Float and big.Rat types can panic if the encoded message is
  too short, potentially allowing a denial of service.

  Found in: math/big@go1.18
  Fixed in: math/big@go1.18.5
  More info: https://pkg.go.dev/vuln/GO-2022-0537

... ...

Vulnerability #9: GO-2021-0052
  Due to improper HTTP header santization, a malicious user can spoof their
  source IP address by setting the X-Forwarded-For header. This may allow
  a user to bypass IP based restrictions, or obfuscate their true source.

  Found in: github.com/gin-gonic/gin@v1.6.3
  Fixed in: github.com/gin-gonic/gin@v1.7.7
  More info: https://pkg.go.dev/vuln/GO-2021-0052
```

我们看到govulncheck输出的信息分为两部分，一部分是扫描出来的项目存在的安全漏洞，针对这些漏洞你必须fix；而另外一部分(由=== Informational === 分隔的)则是列出一些带有安全漏洞的包，这些包是你直接导入或间接依赖的，但是你并未直接调用存在漏洞的包中的函数或方法，因此无需采取任何弥补措施。这样，我们仅需重点关注第一部分信息即可。

根据漏洞所在的宿主不同，第一部分的信息也可以分为两类：一类是Go语言自身(包括Go编译器、Go运行时和Go标准库等)引入的漏洞，另外一类则是第三方包(包括直接依赖的以及间接依赖的)引入的漏洞。

针对这两类漏洞，我们的解决方法有所不同。

第一类漏洞的解决方法十分简单，**直接升级Go版本即可**，比如这里我将我的Go版本从[Go 1.18](https://tonybai.com/2022/04/20/some-changes-in-go-1-18)升级到最新的Go 1.18.6(2022.9.7日刚刚发布的)即可消除上面的所有第一类漏洞。

而第二类漏洞，即第三方包引入的漏洞，消除起来就要仔细考量一番了。

我们也分成两种情况来看：

-   直接依赖包中存在安全漏洞

如果是项目的直接依赖包的代码中有安全漏洞，这种情况较为简单，根据govulncheck的fix提示，直接升级(go get)到对应的版本即可。

-   间接依赖包中存在安全漏洞

假设我们的project依赖A包，而A包又依赖B包，而govulncheck恰恰扫描出B包存在漏洞，且该漏洞所在函数/方法被我们的项目通过A包调用了。这时我们该如何fix呢？

我们可以直接升级B包的版本吗？不确定！这与go module的依赖管理机制有关，go module正确管理的前提是所有包的版本真正符合[semver(语义版本)规范](https://semver.org/)。如果B包没有完全遵守semver规范，一旦单独升级B包版本，这很可能导致A包无法使用升级后的B包而致使我们的项目无法编译通过。在这种情况下，我们应该首先考虑升级A包，如果A包是我们自己可控的基础库，比如common之类的，我们应该先消除A包的漏洞（顺便升级了B包的版本），然后通过升级A包版本来消除这样的漏洞情况。

如果A包并非我们可控的包，而是某个公共开源包，那也要先查找A包是否已经发布了修复B包漏洞的新版本，如果找到了，直接升级A包到新版本即可解决问题。

如果A包没有修复B包的漏洞，那么问题就略复杂了。我们可以尝试升级B包来修复，如果依旧无法修复，那么我们要么给A包提PR，要么fork一份A，自己修复并直接依赖fork后的A。

如果这种间接依赖链比较长，那么修正这样的漏洞的确比较繁琐，大家务必要有耐心地从直接依赖包逐层向下升级依赖包版本。

___

govulncheck工具的推出丰富了我们对项目进行安全漏洞检查的手段。如果你的项目在github上开源的话，还可以使用github每周security alert来获取安全漏洞信息(如下图所示这样)：

![](https://tonybai.com/wp-content/uploads/an-intro-of-govulncheck-3.png)

并且github提供了很便利的一键fix的方案。

对于公司内的私有商业项目，不管你之前用什么工具对[软件供应链](https://tonybai.com/2022/03/14/software-supply-chain-security-in-go)进行安全扫描，现在我们有了govulncheck，建议定期用它扫描一下。

___

[“Gopher部落”知识星球](https://wx.zsxq.com/dweb2/index/group/51284458844544)旨在打造一个精品Go学习和进阶社群！高品质首发Go技术文章，“三天”首发阅读权，每年两期Go语言发展现状分析，每天提前1小时阅读到新鲜的Gopher日报，网课、技术专栏、图书内容前瞻，六小时内必答保证等满足你关于Go语言生态的所有需求！2022年，Gopher部落全面改版，将持续分享Go语言与Go应用领域的知识、技巧与实践，并增加诸多互动形式。欢迎大家加入！

![img{512x368}](http://image.tonybai.com/img/tonybai/gopher-tribe-zsxq-small-card.png)  
![img{512x368}](http://image.tonybai.com/img/tonybai/go-programming-from-beginner-to-master-qr.png)

![img{512x368}](http://image.tonybai.com/img/tonybai/go-first-course-banner.png)  
![img{512x368}](http://image.tonybai.com/img/tonybai/imooc-go-column-pgo-with-qr.jpg)

[我爱发短信](https://51smspush.com/)：企业级短信平台定制开发专家 https://51smspush.com/。smspush : 可部署在企业内部的定制化短信平台，三网覆盖，不惧大并发接入，可定制扩展； 短信内容你来定，不再受约束, 接口丰富，支持长短信，签名可选。2020年4月8日，中国三大电信运营商联合发布《5G消息白皮书》，51短信平台也会全新升级到“51商用消息平台”，全面支持5G RCS消息。

著名云主机服务厂商DigitalOcean发布最新的主机计划，入门级Droplet配置升级为：1 core CPU、1G内存、25G高速SSD，价格5$/月。有使用DigitalOcean需求的朋友，可以打开这个[链接地址](https://m.do.co/c/bff6eed92687)：https://m.do.co/c/bff6eed92687 开启你的DO主机之路。

Gopher Daily(Gopher每日新闻)归档仓库 – https://github.com/bigwhite/gopherdaily

我的联系方式：

-   微博：https://weibo.com/bigwhite20xx
-   博客：tonybai.com
-   github: https://github.com/bigwhite

![](http://image.tonybai.com/img/tonybai/iamtonybai-wechat-qr.png)

商务合作方式：撰稿、出书、培训、在线课程、合伙创业、咨询、广告合作。

© 2022, [bigwhite](https://tonybai.com/). 版权所有.

Related posts:

1.  [聊聊Go语言的软件供应链安全](https://tonybai.com/2022/03/14/software-supply-chain-security-in-go/ "聊聊Go语言的软件供应链安全")
2.  [Go是如何缓解供应链攻击的\[译\]](https://tonybai.com/2022/04/02/how-go-mitigates-supply-chain-attacks/ "Go是如何缓解供应链攻击的[译]")
3.  [Go，12周年](https://tonybai.com/2021/11/11/go-opensource-12-years/ "Go，12周年")
4.  [Gopher部落：2022年要做的事儿](https://tonybai.com/2022/03/06/the-2022-plan-of-gopher-tribe/ "Gopher部落：2022年要做的事儿")
5.  [Go是否支持增量构建？我来告诉你！](https://tonybai.com/2022/03/21/go-native-support-incremental-build/ "Go是否支持增量构建？我来告诉你！")