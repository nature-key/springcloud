1.什么是微服务
 把一个一站式服务，拆分成根据业务的一个个小得服务去耦合，每一个服务负责一种业务，只做一个一件事，技术方面一个小的独立的处理服务，类似进程，可有自己的数据库，可以独立创建销毁，

 2.微服务
  注重一个个个体，具体解决某一个问题，提供的实际服务

 3.微服务架构
 是一个架构模型，把一个应用拆分成一个个服务，服务之间互相协作互相配合，为用户提供最终的价格，每个服务进行独立的进程中，服务之间用轻量级通信restFul api，每个服务有自己的业务，可以独立运行到生产环境，尽量避免集中，统一的服务管理，每个服务可以不用不同语言，工具进行构建

 4.优点
  每个服务足够内聚，足够小，代码容易理解，能够聚焦一个指定的业务功能和业务需求
  开发简单，开发效率提高，一个服务专一只干一件事，
  微服务可以被小团队开发，
  微服务松耦合，是有功能意义的服务，独立开发部署
  不通语言开发
  易于和第三方继承，微服务允许且灵活的方式继承自动部署，通过持续集成工具
  允许你利用融合最新技术，
  只有业务代码，不会和html,css 混合
  独立的数据库
 缺点
 分布式的复杂性
 多服务运维难度高
 系统部署依赖
 服务间通信技术
 数据的一致性
 系统集成测试
 性能监控

 5.springcloud=分布式微服务架构的一站式解决方案，是微服务架构的技术的集合体，
 6.sprigcloud和springboot关系

   springboot是指一个个服务，微观的，sprigcloud是指整个微服务，宏观的
   springboot相当医院的每一个科室，springcloub相当整个医院，
  springboot专注快速开发单个个体服务，
  springcloud关注全局的微服务协调整治框架，他讲springboot开发的一个个服务整个起来管理
  为各个服务之间提供集成服务
  springboot可以单独运行部署，springcloud依赖springboot

  springboot专注于块苏，方便开发单个微服务个体，springcloud整个微服务治理框架
 
  7.Eureka
  Eureka是Netflix的子模块，也是核心模块，用用服务的定位，是云端后中间件的服务发现与故障转移，服务的发现和注册非常重要，只要知道服务的标识，就可以找到服务，和dubbo的注册中心一样类zookeer
  8.Eureka自我保护模式
   默认情况下，如果EurekaServer在一定时间没有接受某个微服务的实例心跳，EureksServer将会注销实例（默认90秒），但是当网络分区出现故障时，为鼓舞和EurekaSERVER无法通讯，Eureks进入自我保护模式，来解决这个问题，当EurekaServer节点短时间丢失多客户端，呢么这个节点就进入自我保护模式，一旦进入这模式，Eureks救赎保护服务祖册表中的信息，不在删除服务注册表的数据，当网络故障恢复后，该Eureka Server节点会退出子自我保护模式
   9.zookeeper h和eureka

    1.zookeeper 使用CP(一致性 分布区容错行)
    当想注册中心查询功能，我们可以容忍注册中心返回几分钟以前的信息，但是不能接受直接down不可用，也就是说，服务注册功能可用性要求高于以后一致性，按时zk会初心这一种情况，当master出现故障，和其他节点失去联系下，剩余节点重新选举leader，问题是，选举时间在30-120s,选举期间不可用，这导致选举期间注册服务瘫痪，在与部署的环境下，因网络问题使得zk集群失去master节点是交大概率发生的事，虽然做种可以恢复，但是漫长的选举时间导致注册长时间不可用是不能容忍的，
    2.eureka 使用AP(高可用 分布式容错行)
     优先保证可用性，Eureka各个节点都是平等，结果几点过掉不会影响正常节点的工作，食欲节点依然可以提供注册，和查询服务，而Eureka的客户端在某个Eureka注册时如果发现连接失败，自动切换至其他正常的节点，只要有一台还在，就可以保证可用性，但是查询的信息可能不是最新的，eureka有自我保护模式，在某段时间没有正常的心跳，eureka认定客户端与注册中心出现了网络故障，
     1.eureka不会移除长时间没有心跳的的服务，而应该过期的服务
     2.EUREKA仍然能够接受注册和查询请求，但是不会同步其他的节点
     3.当网络稳定时，当前实例新的祖册信息会被注册到其他节点，
  10,负载均衡
    Load Balance ,负载均衡，在微服务的或分布式进程用到
    简单来说就是把请求平摊到服务器上，是服务达到高可用
    常用的工具 Nginx LVS ,硬件F5，
    还有以下中间件如dubbo,springcloud ，而且springcloud 都是可以自动以负载均衡算法
   集中式LB
     服务的消费者和提供方之间使用独立的LB设施（硬件 F5 也可以是软件Nginx）,由改设施负责吧访问请求通过某种策略准发到服务提供方；
   进程内LB
   将LB逻辑集成到消费方，消费方冲注册中心获取那些地址可用，然后寻出一个合适的服务器，
   Ribbon 就属于进程内LB，他属于一个类库，继承与消费方进程，消费方通过他来获取服务提供放的地址
  11.Feign
   Fegin是一个声明式的web服务客户端，是的编写WEB服务客户端变的非常简单
   只需要创建一个接口，然后在上面添加注解即可
    Fegin怎么出来的
    1.直接调用微服务来进行访问
    2，目前习惯面向接口编程，比如webserver接口， DAO接口
      2.1 微服务名称获得调用地址
      2.2 通过接口和注解
        如DAO
   Fegin能干什么

   是java编写客户端更加容易
   前面在使用Ribben 和 RestTemplate ,医用RestTmplate 的对http请求的封装处理，形成一套模块化调用方法，但是是家中
   由于微服务依赖的调用可能不止一处，旺旺接口的调用不止一处，所以通常都会针对每一个微服务自行封装一些客户端类。包装
   这些依赖的服务的调用，多以Fegin在此基础上进一步封装，由他来帮助我们定义实现依赖服务接口的定义，在Feign实现下，我们只
   需创建一个接口并使用注解的方式来配置他，即可完成对服务提供方的接口绑定，简化了使用 spring CLOUD Ribbon 时，自动
   封装服务调用客户端的开发量
   12.Hystrix
     Hystrix是一个用于处理分布式系统的延迟和容错的开源库，在分布式系统里，许多依赖不可避免的会调用失败，比如超时，异常等，Hystrix是一个保证在一个依赖出现问题的情况下，不会导致整体服务失败，避免级联故障，以提高分布式系统的弹性。
     “断路器”本身是一种开关装置，当某个服务单元发生故障之后，通过断路器的故障监控，向调用方返回一个符合预期的，可以处理的备选响应，而不是长时间的等待或者抛出调用者应用者无法处理的异常，这样就保证服务调用方的线程不会被长时间，不必要的占用，从而避免故障在分布式系统的蔓延，乃至雪崩
     服务熔断
      一般一个服务故障或异常引起，类似显示生活中的保险丝，当某个异常条件被处罚，知道熔断整个服务，而不是一直等到服务超时

     Hystyix服务降级
     整体资源快不够用了，热痛将某些服务先关掉，待度过难关，在开启回来

     所谓降级，一般冲整体符负荷考虑，就是当某个服务熔断之后，富将步子啊被调用

     此时客户端可以自己准备一个本地 fallback回调，返回一个缺省值

     这样做，虽然服务水平下降，，单号地可用，比直接挂掉好

     Hystrix dashboard

     实心圆：两种含义 他通过颜色变化代表了实例的健康，他的健康冲 绿 黄 橙 红 递减

      该实心圆除了颜色变化，还有大小，根据实例的请求量发生变化，流量越大实心圆越大，他通过实心圆的展示，就可以在大量的实例中发现
      古装实例的和高压力实例
    Zuul包含对请求的路由和过滤两个功能
     孩子请理由功能负责将外部请求转发到具体的微服务实例上，是实现外部访问统一入口的基础而过滤器功能则负责对请求的处理过程进行干扰
     是实现请求校验，服务聚合等功能的基础，Zuul和Eureka进行整合，将Zuul自身初测为Eureka服务治理下的应用，同时冲Eureka,中获取其他微服务的消息，也即有的访问微服务都是通过Zuul跳转后获得
         Zuul服务最终还是会注册进Eureka


    提供=代理+路由+过滤
    
    MICROSERVICECLOUD-DEPT

    13 Springcloud Config 
      为微服务架构中的微服务提供集中化外部配置支持，配置服务器为各个不同微服务应用的所有环境提供了一个中心化外部配置     





































