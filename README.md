# javaee7-samples
集合了160个javaEE的融合
JavaEE7 事例

此工作区包含的Java EE 7的样品和单元测试。他们被分为不同的目录，每个技术/ JSR。

部分样本/测试有文件，否则读取的代码。在JavaEE7大要素的书是指大多数这些样品，并提供一个解释。随意添加文档发送pull请求。

如何运行？

样品在Wildfly和GlassFish使用的Arquillian生态系统进行测试。

简要说明如何克隆，构建，进口和在本地机器上运行@radcortez样本提供了在此示例视频https://www.youtube.com/watch?v=BB4b-Yz9cF0

只有一个集装箱的个人资料和浏览器的一个配置文件可以在特定时间被激活，否则就会有依赖性的冲突。

有10个可用容器外形，为5个不同的服务器：

wildfly-managed-arquillian

此配置文件将安装一个Wildfly服务器并启动每次采样的服务器。有用的CI服务器。

wildfly-embedded-arquillian

该配置文件几乎是相同的wildfly管理-的Arquillian。它将安装在同一Wildfly服务器和再次启动每采样该服务器，而是使用的Arquillian嵌入式连接到在相同的JVM运行它。有用的CI服务器。

wildfly-remote-arquillian

此配置文件需要你构建之外启动一个Wildfly服务器。然后，每个样本将重用这个实例来运行测试。有用的发展，以避免在服务器启动每个样品的成本。这是默认的配置文件。

glassfish-embedded-arquillian

该配置文件使用了GlassFish嵌入式服务器，并在同一JVM中的TestClass运行。有用的发展，但每个样本服务器启动的缺点。

glassfish-remote-arquillian

此配置文件需要你构建之外启动一个GlassFish服务器。然后，每个样本将重用这个实例来运行测试。有用的发展，以避免在服务器启动每个样品的成本。

tomee-managed-arquillian

此配置文件将安装一个TomEE服务器，并启动每个样品该服务器。有用的CI服务器。此配置文件无法连接到正在运行的服务器。

注意，要使用的TomEE的版本有存在于一个可用行家存储库。在此配置文件的默认假设的Arquillian适配器和TomEE服务器具有相同的版本。如双方7.0.0。

要使用TomEE服务器，这不是在Maven中可用的中央，一个办法使用它的样本如下：安装在一个地方.m2目录：

克隆TomEE回购：

git clone https://github.com/apache/tomee cd tomee

切换到所需的版本，如果需要的话，那么建立和安装的.m2：

mvn clean install -pl tomee/apache-tomee -am -Dmaven.test.skip=true

mvn clean install -pl arquillian -amd -Dmaven.test.skip=true

确保已安装（见TomEE项目pom.xml中）的版本相匹配的tomee.version在样本项目的根pom.xml中属性部分。

tomee-embedded-arquillian

此配置文件使用TomEE嵌入式服务器，并在同一JVM中的TestClass运行。

liberty-managed-arquillian

此配置将启动每次采样的自由服务器，以及任选连接到可以构建的外启动（与该服务器具有到主机上运行作为其中测试使用相同的用户运行限制一个运行的服务器）。

要连接到正在运行的服务器的org.jboss.arquillian.container.was.wlp_managed_8_5.allowConnectingToRunningServer 系统属性已被设置为true。例如

-Dorg.jboss.arquillian.container.was.wlp_managed_8_5.allowConnectingToRunningServer=true

此配置文件需要您设定在自由通过安装的位置libertyManagedArquillian_wlpHome 的系统属性。例如

-DlibertyManagedArquillian_wlpHome=/opt/wlp

此配置文件还要求localConnector功能在server.xml中进行配置，如果所有测试将要运行的JavaEE的-7.0功能例如：

< 的FeatureManager >
    < 功能 >的JavaEE-7.0 </ 功能 >
    < 特点 > localConnector-1.0 </ 功能 >
</ 的FeatureManager >
对于JASPIC测试，甚至可以尝试执行的作弊需要创建在自由的内部用户注册表组：

< basicRegistry  ID = “基本” >
    < 组 名 = “建筑师” />
</ basicRegistry >
liberty-embedded-arquillian

此配置文件会下载并安装一个自由服务器并启动每次采样的服务器。有用的CI服务器。注意，这不是一个实际的嵌入式服务器，但常规服务器。它现在被称为“嵌入”，因为，因为它是自动下载没有单独的需要进行安装。

weblogic-remote-arquillian

此配置文件需要你构建之外启动一个WebLogic Server中。然后，每个样本将重用这个实例来运行测试。注意：这已经在WebLogic 12.1.3，这是一个Java EE 6的实施测试，但它有一些Java EE 7的功能，可以有选择地激活。

此配置文件需要您设置在哪里的WebLogic通过安装的位置weblogicRemoteArquillian_wlHome 的系统属性。例如

-DweblogicRemoteArquillian_wlHome=/opt/wls12130

默认的用户名/密码被假定为“admin”和“admin007”分别。这可以使用被改变 weblogicRemoteArquillian_adminUserName和weblogicRemoteArquillian_adminPassword系统性能。例如

-DweblogicRemoteArquillian_adminUserName=myuser -DweblogicRemoteArquillian_adminPassword=mypassword

一些容器允许您覆盖使用的版本

-Dorg.wildfly=8.1.0.Final

这将版本8.0.0从改变8.1.0.Final为WildFly。

-Dglassfish.version=4.1

这会从4.1.1版本改为4.1 GlassFish的测试目的。

同样，也有6个配置选择浏览器上测试：

browser-firefox

要运行在Mozilla Firefox的测试。如果它的二进制被安装在通常的位置，则不需要附加信息。

browser-chrome

要运行在谷歌浏览器的测试。需要一个传递-Darq.extension.webdriver.chromeDriverBinary属性指向一个chromedriver二进制文件。

browser-ie

要运行在Internet Explorer的测试。需要一个传递-Darq.extension.webdriver.ieDriverBinary属性指向IEDriverServer.exe。

browser-safari

在Safari上运行测试。如果它的二进制被安装在通常的位置，则不需要附加信息。

browser-opera

在Opera上运行测试。需要一个传递-Darq.extension.webdriver.opera.binary属性指向一个歌剧的可执行文件。

browser-phantomjs

要运行模拟浏览器PhantomJS测试。如果不通过指定phantomjs二进制文件的路径 -Dphantomjs.binary.path属性时，它会自动下载。

要在控制台中运行他们这样做：

在终端，mvn -Pwildfly-managed-arquillian,browser-firefox test在顶层目录来启动测试
当开发和IDE乳宁他们，记得运行测试之前启动的情景。

要了解更多有关的Arquillian请参阅的Arquillian指南

要仅运行测试的一个子集做的顶级目录：

安装顶级的依赖关系： mvn clean install -pl "test-utils,util" -am
cd到所需模块，如： cd jaspic
针对运行所需的服务器，例如测试： mvn clean test -P liberty-embedded-arquillian
如何贡献

有了您的帮助，我们可以改善这组样品，相互学习和成长的社会各界全面谁关心技术，创新和代码质量激情的人。每个做出贡献的问题！

只是有一堆东西，你应该记住发送拉请求之前，所以我们可以很容易地得到所有纳入主分支的新事物。

标准测试是基于JUnit的-比如这次提交。测试类的命名必须符合神火命名标准**/*Test.java，**/*Test*.java或**/*TestCase.java。

但是，如果你喜欢新的东西，髋关节和时尚是完全合法的写斯波克的规格为标准的JavaEE集成测试。为了清晰和一致性起见，尽量减少前期的复杂性，在这个项目中，我们prefare标准的JUnit测试。然而，在提供了一些斯波克例如extra/spock-tests文件夹- 喜欢这里。该spock-tests项目还展示了Maven配置。在这种特殊情况下Groovy的规范文件包含在Maven的测试阶段，当且仅当您按照斯波克命名约定，让你的Specification后缀魔术会发生。

Extras文件夹默认是不包括在内，以限制Groovy的依赖。如果要导入额外的样本在Eclipse工作区（包括斯波克测试），请安装Groovy的插件Eclipse版本，然后再导入您想使用文件示例项目>导入>现有Maven项目。

一些编码原则

当创建新的源文件不要放在（或复制）任何牌照的头，因为我们使用的每个顶级许可证（MIT），并在这个仓库的所有文件。
请按照JBoss的社区代码格式化配置文件，如定义的JBoss / IDE-配置存储库。的细节进行说明那里，以及为Eclipse，的IntelliJ和NetBeans配置。
小提示的Git

确保您的前叉始终是最新的。只需运行git pull upstream master，你准备好砍。
在开发新的功能，请创建一个特性分支，使我们顺利地融入您的更改。这也方便了你，你可以在并行几件事情工作;）为了创建一个特性分支，并切换到它一举你可以使用git checkout -b my_new_cool_feature
而已！欢迎社会！

CI工作

WildFly
GlassFish的
TomEE
运行泊坞窗每个样本

从安装客户端泊坞窗http://boot2docker.io/
构建要为运行示例

mvn clean package -DskipTests

例如：

mvn -f jaxrs/jaxrs-client/pom.xml clean package -DskipTests

在更改第二行Dockerfile指定生成的WAR文件的位置

运行boot2docker并给出命令

docker build -it -p 80:8080 javaee7-sample

在不同的外壳，找出运行的容器作为的IP地址：

boot2docker ip

访问示例为http：// IP地址：80 / JAXRS客户端/ webresources /人。确切的URL会有所不同凭样品。
