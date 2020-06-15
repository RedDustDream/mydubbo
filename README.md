# mydubbo 
学习使用dubbo
dubbo注册服务，服务发现，集群。
操作步骤：
1.下载并启动zookeeper
下载springboot版的zookeeper应用,java -jar 启动zookeeper
2.启动dubbo
下载springboot版的dubbo应用，java -jar 启动dubbo
3.创建提供者，消费者，3.1-3同时两者都适用
3.1 添加依赖 pom.xml
<!-- https://mvnrepository.com/artifact/com.alibaba.boot/dubbo-spring-boot-project -->
		<dependency>
			<groupId>com.alibaba.boot</groupId>
			<artifactId>dubbo-spring-boot-project</artifactId>
			<version>0.2.1</version>
			<type>pom</type>
		</dependency>
		<!-- https://mvnrepository.com/artifact/com.101tec/zkclient -->
		<dependency>
			<groupId>com.101tec</groupId>
			<artifactId>zkclient</artifactId>
			<version>0.11</version>
		</dependency>
		<!-- https://mvnrepository.com/artifact/com.alibaba/dubbo -->
		<dependency>
			<groupId>com.alibaba</groupId>
			<artifactId>dubbo</artifactId>
			<version>2.6.2</version>
		</dependency>
		<dependency>
			<groupId>org.apache.curator</groupId>
			<artifactId>curator-framework</artifactId>
			<version>2.12.0</version>
		</dependency>
		<dependency>
			<groupId>org.apache.zookeeper</groupId>
			<artifactId>zookeeper</artifactId>
			<version>3.4.10</version>
			<exclusions>
				<exclusion>
					<groupId>org.slf4j</groupId>
					<artifactId>slf4j-log4j12</artifactId>
				</exclusion>
				<exclusion>
					<groupId>log4j</groupId>
					<artifactId>log4j</artifactId>
				</exclusion>
			</exclusions>
		</dependency>
	</dependencies>
3.2 配置参数 application.properties
    #dubbo服务端口，我们无需知道dubbo服务运行在哪个端口，故也将其设为随机端口
    dubbo.protocol.port = -1
    dubbo.protocol.name = dubbo
    #dubbo服务名称
    dubbo.application.name = dubbo-provider
    #dubbo服务所在包路径
    dubbo.scan.basePackages  = com.hj
    #注册中心地址
    dubbo.registry.address=zookeeper://IP:2181
3.3 启动类上增加注解 @EnableDubbo
提供者：
3.4 暴露的接口实现类上增加注解 @Service（com.alibaba.dubbo.config.annotation.Service;） @Component（org.springframework.stereotype.Component;）
消费者：前面同3.1-3
3.5 在消费的接口上增加注解，同3.4
3.6 在controller层，使用@Reference（com.alibaba.dubbo.config.annotation.Reference;）注解注入对象，不需要使用@Autowired

