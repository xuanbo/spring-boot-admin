## spring boot usage

> base on spring boot admin 1.5.x

* admin-server(spring boot admin server)
* admin-client(spring boot admin client)

### admin-server

#### dependencies

```xml
<dependencies>
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
</dependencies>
```

#### application.yml

```yml
server:
  # only export server port
  port: 8081
```

### admin-client

#### dependencies

```xml
<dependency>
    <groupId>de.codecentric</groupId>
    <artifactId>spring-boot-admin-starter-client</artifactId>
    <version>${admin.version}</version>
</dependency>
```

#### application.yml

```yml
server:
  # export client port
  port: 8080

spring:
  boot:
    admin:
      # admin server url
      url: http://localhost:8081
management:
  security:
    # enable security
    enabled: false
```

### run

* run admin-server
* run admin-client

open browser: `http://localhost:8081`