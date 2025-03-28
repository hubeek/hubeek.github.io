# build jar with namen in maven

_Status: Published_
_Created: 2020-12-11 02:44:12_

```
<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-jar-plugin</artifactId>
				<version>3.2.0</version>
				<configuration>
					<finalName>scraper</finalName>
				</configuration>
			</plugin>
		</plugins>
	</build>
```