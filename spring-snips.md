# Spring snips

_Status: Published_
_Created: 2024-08-28 03:59:02_
_Tags: spring, java_

## Docker
### local
```
docker run -v ./app.jar:/app/app.jar \
-e DB_USERNAME='admin' -e DB_PASSWORD='password123' \
-p 8080:8080 \
amazoncorretto:21 \
java -jar /app/app.jar --spring.profiles.active=prod
```

## start met .properties file 
```
DB_USERNAME=user java -jar target/app.jar --spring.profiles.active=prod
```
## Application properties
in application.prod.properties
```
spring.application.version=@project.version@

// h2
spring.datasource.username=${DB_USERNAME}
spring.datasource.password=${DB_PASSWORD}
spring.datasource.url=jdbc:h2:mem:contactdb
spring.h2.console.enabled=true

// MySQL
spring.datasource.url=jdbc:mysql://localhost:3306/tempdb?useUnicode=true&useLegacyDatetimeCode=false&serverTimezone=UTC&createDatabaseIfNotExist=true&allowPublicKeyRetrieval=true&useSSL=false
spring.datasource.username=root
spring.datasource.password=<YOURPASS>
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# Hibernate JPA settings
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLDialect
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

# Logging level for debugging
logging.level.org.hibernate=DEBUG

logging.level.root=debug

```

## actuator
voor in dev:
```
management.endpoints.web.exposure.include=*
management.endpoint.health.show-details=always
management.server.port=9090
```

## Intellij Endpoint POST Request
```
POST http://localhost:8080/players
Accept: */*
Accept-Encoding: gzip, deflate
Content-Type: application/json
Accept-Language: en-us

{
 "role" : "value3",
 "name": "value4"
}

```

## Lombok
### Log4j2 Pattern Layout Alternative
configure Log4j2 to automatically include the class and method names in log messages by setting up a custom pattern in log4j2.xml:
```
<PatternLayout pattern="%d{yyyy-MM-dd HH:mm:ss} %-5p [%t] %C{1}.%M - %msg%n"/>

```

## Swagger
``
<dependency>
            <groupId>org.springdoc</groupId>
            <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
            <version>2.6.0</version>
        </dependency>
```
```
http://localhost:8080/swagger-ui/index.html

en json format
http://localhost:8080/v3/api-docs
```

## Profiles

in yaml -- maakt er feitelijk 2 yaml docs van

in .properties:
```
spring.profiles.active=sql
spring.config.activate.on-profile=sql
```

## Kafka
`https://kafka.apache.org/quickstart`
```
// download
10015  tar -xzf kafka_2.13-3.8.0.tgz
// unpack and start
10016  cd kafka_2.13-3.8.0
10019  cd ~/Downloads/kafka_2.13-3.8.0
10020  bin/kafka-server-start.sh config/server.properties
10022  bin/kafka-topics.sh --create --topic quickstart-events --bootstrap-server localhost:9092
10023  bin/kafka-topics.sh --describe --topic quickstart-events --bootstrap-server localhost:9092
10024  bin/kafka-console-producer.sh --topic quickstart-events --bootstrap-server localhost:9092
10026  bin/kafka-console-consumer.sh --topic quickstart-events --from-beginning --bootstrap-server localhost:9092
10027  bin/kafka-server-start.sh config/server.properties
// consume
10029  bin/kafka-console-producer.sh --topic quickstart-events --bootstrap-server localhost:9092
10030  bin/kafka-console-consumer.sh --topic quickstart-events --from-beginning --bootstrap-server localhost:9092
10032  bin/kafka-topics.sh --describe --topic cab-location --bootstrap-server localhost:9092
10033  bin/kafka-console-consumer.sh --topic cab-location --from-beginning --bootstrap-server localhost:9092

```
## application properties Driver
```
spring.application.name=kafkaBookingDriver
spring.kafka.producer.bootstrap-servers=localhost:9092
spring.kafka.producer.key-serializer=org.apache.kafka.common.serialization.StringSerializer
spring.kafka.producer.value-serializer=org.apache.kafka.common.serialization.StringSerializer
server.port=8082

```

## application properties User
```
spring.application.name=kafkaBookingUser

spring.kafka.consumer.bootstrap-servers=localhost:9092
spring.kafka.consumer.key-serializer=org.apache.kafka.common.serialization.StringSerializer
spring.kafka.consumer.value-serializer=org.apache.kafka.common.serialization.StringSerializer
spring.kafka.consumer.auto-offset-reset=earliest
server.port=8081

spring.kafka.consumer.group-id=user-group

```
## Driver
needs:
- config  

- Controller  

- service  


config:
```
package nl.appall.java.spring.kafkabookingdriver.config;

import org.apache.kafka.clients.admin.NewTopic;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.kafka.config.TopicBuilder;

import static nl.appall.java.spring.kafkabookingdriver.constant.AppConstant.CAB_LOCATION;

@Configuration
public class KafkaConfig {


    @Bean
    public NewTopic topic() {
        return TopicBuilder
                .name(CAB_LOCATION)
                .build();
    }
}
```

controller:
```
package nl.appall.java.spring.kafkabookingdriver.controller;

import nl.appall.java.spring.kafkabookingdriver.service.CabLocationService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.Map;

@RestController
@RequestMapping("/location")
public class CabLocationController {

    @Autowired private CabLocationService cabLocationService;

    @PutMapping
    public ResponseEntity updateLaction() throws InterruptedException {

        int range = 100;
        while(range > 0) {
            cabLocationService.updateLocation(Math.random() + " , "+ Math.random());
            Thread.sleep(1000);
            range--;
        }
        return new ResponseEntity<>(Map.of("message","Location Updated"), HttpStatus.OK);
    }
}
```
service:
```
package nl.appall.java.spring.kafkabookingdriver.service;

import nl.appall.java.spring.kafkabookingdriver.constant.AppConstant;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.kafka.core.KafkaTemplate;
import org.springframework.stereotype.Service;

@Service
public class CabLocationService {

    @Autowired private KafkaTemplate<String,Object> kafkaTemplate;

    public boolean updateLocation(String location){
        kafkaTemplate.send(AppConstant.CAB_LOCATION, location);
        return true;
    }
}

```


## User
needs only service
```
package nl.appall.java.spring.kafkabookinguser;

import org.springframework.kafka.annotation.KafkaListener;
import org.springframework.stereotype.Service;

@Service
public class LocationService {

    @KafkaListener(
            topics = "cab-location",
            groupId = "user-group"
    )
    public void cabLocation(String location){
        System.out.println(location);

    }
}

```

