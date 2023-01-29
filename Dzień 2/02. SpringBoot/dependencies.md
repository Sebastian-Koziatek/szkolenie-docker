# Java jdk-19

```bash
wget https://download.oracle.com/java/19/latest/jdk-19_linux-x64_bin.deb

sudo apt-get -qqy install ./jdk-19_linux-x64_bin.deb

sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk-19/bin/java 1919
```

# Plik SzkolenieApplicationTests.java

Podmień zawartość pliku Aplikacja/src/main/SzkolenieApplication.java

```java
package com.example.demo;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@SpringBootApplication
@RestController
public class SzkolenieApplication {

  @RequestMapping("/")
  public String getHome() {
    return "Szkolenie docker - aplikacja java zbudowana na spring";
  }
  @RequestMapping("/messages")
  public String getMessage() {
    return "Hello Messages Endpoint";
  }

  public static void main(String[] args) {
    SpringApplication.run(SzkolenieApplication.class, args);
  }

}
```
___