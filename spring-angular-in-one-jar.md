# Spring + Angular in one jar

_Status: Published_
_Created: 2021-07-23 07:18:19_
_Tags: spring, angular, maven_

based on:  
[Webapp with Create React App](https://www.kantega.no/blogg/webapp-with-create-react-app-and-spring-boot)

- create spring app
- prevent cors
```
@Bean
    public WebMvcConfigurer corsConfigurer() {
        return new WebMvcConfigurer() {
            @Override
            public void addCorsMappings(CorsRegistry registry) {
                registry.addMapping("/**")
                        .allowedOrigins("http://localhost:4200")
                        .allowedHeaders("application/json", "text/plain", "*/*",
                                "Access-Control-Allow-Headers",
                                "Access-Control-Allow-Origin",
                                "Origin", "Accept", "X-Requested-With, Content-Type",
                                "Access-Control-Request-Method",
                                "Access-Control-Request-Headers")
                        .allowedMethods("GET", "PUT", "POST", "PATCH", "DELETE", "OPTIONS")
                        .maxAge(3600)
                ;
            }
        };

```
- in root create new ng app
- create proxy.conf.json in root frontend app
```
{
  "/api/*": {
    "target": "http://localhost:8080",
    "secure": false,
    "logLevel": "debug",
    "changeOrigin": true
  }
}
```
- change angular.json:
```
            "development": {
              "browserTarget": "frontend:build:development",
              "proxyConfig": "proxy.conf.json"
            }
```
- add plugin for building the frontend:  
**note: version!!!**  
**note: npmVersion!!!**  
**note: nodeVersion!!!**  
```
<plugin>
                <groupId>com.github.eirslett</groupId>
                <artifactId>frontend-maven-plugin</artifactId>
                <version>1.9.1</version>
                <configuration>
                    <workingDirectory>frontend</workingDirectory>
                    <installDirectory>target</installDirectory>
                </configuration>
                <executions>
                    <execution>
                        <id>install node and npm</id>
                        <goals>
                            <goal>install-node-and-npm</goal>
                        </goals>
                        <configuration>
                            <nodeVersion>v14.15.4</nodeVersion>
                            <npmVersion>7.17.0</npmVersion>
                        </configuration>
                    </execution>
                    <execution>
                        <id>npm install</id>
                        <goals>
                            <goal>npm</goal>
                        </goals>
                        <configuration>
                            <arguments>install</arguments>
                        </configuration>
                    </execution>
                    <execution>
                        <id>npm run build</id>
                        <goals>
                            <goal>npm</goal>
                        </goals>
                        <configuration>
                            <arguments>run build</arguments>
                        </configuration>
                    </execution>
                </executions>
            </plugin>

```
- copy the dist version to target:  
**note double check location where the build is located**  
**note mvn clean package**  
```
<plugin>
                <artifactId>maven-antrun-plugin</artifactId>
                <executions>
                    <execution>
                        <phase>generate-resources</phase>
                        <configuration>
                            <target>
                                <copy todir="${project.build.directory}/classes/public">
                                    <fileset dir="${project.basedir}/frontend/dist"/>
                                </copy>
                            </target>
                        </configuration>
                        <goals>
                            <goal>run</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
```