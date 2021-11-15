# java

## maven

generate jar from maven project

create src/main/resources/META-INF/MANIFEST.MF

contents below(must contains new line)

```

Main-Class: org.example.App


```

in pom.xml file

add contents below

```

<project>
  ...
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-jar-plugin</artifactId>
        ...
        <configuration>
          <archive>
            <manifestFile>src/main/resources/META-INF/MANIFEST.MF</manifestFile>
          </archive>
        </configuration>
        ...
      </plugin>
    </plugins>
  </build>
  ...
</project>

```

In the **Maven** tool window, in the **Lifecycle** list, double-click the **install** command to generate the **jar** file. IntelliJ IDEA generates the appropriate information in the target folder and an executable JAR in the **Project** tool window.