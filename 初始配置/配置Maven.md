一、修改maven的配置文件settings.xml中的localRepository   
`
<localRepository>Z:\eclipse-jee-2018-12-R-win32-x86_64\eclipse-workspace\taotao\repository</localRepository>
`  
设置自动下载的jar包存储位置  
二、修改maven的配置文件settings.xml中的镜像，请求中央仓库自动下载jar包  
```
<mirror>    
     <id>nexus-aliyun</id>    
     <mirrorOf>central</mirrorOf>  
	 <name>Nexus aliyun</name>  
	 <url>http://maven.aliyun.com/nexus/content/groups/public</url>  
     </mirror>
```
配置国内的阿里云镜像  
三、新建一个maven工程  
```
<groupId>shirley.usermanage</groupId>
  <artifactId>usermanage</artifactId>
  <version>1.0.0-SNAPSHOT</version>
  <packaging>war</packaging>//SSM环境
```
四、继承集中定义依赖版本号的maven  
Import Existing Maven Projects ->parent   
```
<parent>
  <groupId>shirley.parent</groupId>
	<artifactId>parent</artifactId>
	<version>0.0.1-SNAPSHOT</version>
  </parent>
```
五、从父Maven的pom.xml中拷贝需要的依赖
```
  <dependencies>
  			<dependency>
				<groupId>junit</groupId>
				<artifactId>junit</artifactId>
				<scope>test</scope>
			</dependency>
  			<dependency>
				<groupId>org.springframework</groupId>
				<artifactId>spring-webmvc</artifactId>
			</dependency>
			<dependency>
				<groupId>org.springframework</groupId>
				<artifactId>spring-jdbc</artifactId>
			</dependency>
			<dependency>
				<groupId>org.springframework</groupId>
				<artifactId>spring-aspects</artifactId>
			</dependency>
			<dependency>
				<groupId>org.mybatis</groupId>
				<artifactId>mybatis</artifactId>
			</dependency>
			<dependency>
				<groupId>org.mybatis</groupId>
				<artifactId>mybatis-spring</artifactId>
			</dependency>
			<dependency>
				<groupId>mysql</groupId>
				<artifactId>mysql-connector-java</artifactId>
			</dependency>
			<dependency>
				<groupId>org.slf4j</groupId>
				<artifactId>slf4j-log4j12</artifactId>
			</dependency>
			<dependency>
				<groupId>com.fasterxml.jackson.core</groupId>
				<artifactId>jackson-databind</artifactId>
			</dependency>
			<dependency>
				<groupId>com.jolbox</groupId>
				<artifactId>bonecp-spring</artifactId>
			</dependency>
			<dependency>
				<groupId>jstl</groupId>
				<artifactId>jstl</artifactId>
			</dependency>
			<dependency>
				<groupId>javax.servlet</groupId>
				<artifactId>servlet-api</artifactId>
				<scope>provided</scope>
			</dependency>
			<dependency>
				<groupId>javax.servlet</groupId>
				<artifactId>jsp-api</artifactId>
				<scope>provided</scope>
			</dependency>
			<dependency>
				<groupId>org.apache.commons</groupId>
				<artifactId>commons-lang3</artifactId>
			</dependency>
			<dependency>
				<groupId>org.apache.commons</groupId>
				<artifactId>commons-io</artifactId>
			</dependency>
  </dependencies>
  
```  
六、配置Tomcat插件  
```
<build>
  			<plugins>
				<!-- 配置Tomcat插件 -->
				<plugin>
					<groupId>org.apache.tomcat.maven</groupId>
					<artifactId>tomcat7-maven-plugin</artifactId>
					<configuration>
					<port>80</port>
					<path>/</path>
					</configuration>
				</plugin>
				
				   
			</plugins>	
  </build>
```  
七、配置Run Configuration  
Base directory:${workspace_loc:/usermanage}  
Goals:tomcat7:run  
