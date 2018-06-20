## spring cloud usage

> base on spring boot admin 1.5.x

* cloud-discovery(spring cloud eureka server)
* cloud-admin-server(spring cloud admin server)
* cloud-admin-client(spring cloud admin client)

### cloud-discovery

#### dependencies

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-eureka-server</artifactId>
    <version>${spring.cloud.version}</version>
</dependency>
```

#### application.yml

```yml
server:
  port: 8761

spring:
  application:
    name: cloud-discovery

eureka:
  client:
    register-with-eureka: false
    fetch-registry: false
    serviceUrl:
      defaultZone: http://localhost:${server.port}/eureka/
```

#### application

```java
@EnableEurekaServer
@SpringBootApplication
public class DiscoveryApplication {

    public static void main(String[] args) {
        SpringApplication.run(DiscoveryApplication.class, args);
    }

}
```

### cloud-admin-server

also eureka client

#### dependencies

```xml
<dependency>
    <groupId>de.codecentric</groupId>
    <artifactId>spring-boot-admin-server</artifactId>
    <version>${admin.version}</version>
</dependency>
<dependency>
    <groupId>de.codecentric</groupId>
    <artifactId>spring-boot-admin-server-ui</artifactId>
    <version>${admin.version}</version>
</dependency>

<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-eureka</artifactId>
    <version>${spring.cloud.version}</version>
</dependency>
```

#### application.yml

```yml
server:
  port: 8081

spring:
  application:
    name: cloud-admin-server
eureka:
  instance:
    leaseRenewalIntervalInSeconds: 10
  client:
    registryFetchIntervalSeconds: 5
    serviceUrl:
      defaultZone: ${EUREKA_SERVICE_URL:http://localhost:8761}/eureka/

management:
  security:
    enabled: false
```

#### application

```java
@EnableAdminServer
@SpringBootApplication
public class AdminServerApplication {

    public static void main(String[] args) {
        SpringApplication.run(AdminServerApplication.class, args);
    }

}
```

### admin-client

also eureka client

#### dependencies

```xml
<dependency>
    <groupId>de.codecentric</groupId>
    <artifactId>spring-boot-admin-client</artifactId>
    <version>${admin.version}</version>
</dependency>

<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-eureka</artifactId>
    <version>${spring.cloud.version}</version>
</dependency>
```

#### application.yml

```yml
server:
  port: 8080

spring:
  application:
    name: cloud-admin-client
eureka:
  client:
    serviceUrl:
      defaultZone: http://localhost:8761/eureka/
management:
  security:
    enabled: false
```

#### application

```java
@SpringBootApplication
public class AdminClientApplication {

    public static void main(String[] args) {
        SpringApplication.run(AdminClientApplication.class, args);
    }

}
```

### run

* run cloud-discovery
* run cloud-admin-server
* run cloud-admin-client

open browser: `http://localhost:8081`