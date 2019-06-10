---
title: Azure Java 개발을 위해 JDK와 함께 Docker 이미지 사용
description: ''
author: bmitchell287
manager: douge
ms.author: brendm
ms.date: 4/9/2019
ms.devlang: java
ms.topic: conceptual
ms.openlocfilehash: ee8df2a08b23d090965cb42e2c15b934d4785e7c
ms.sourcegitcommit: 03379369346974c6e80f86e7129b885112b5c1a9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/29/2019
ms.locfileid: "64910236"
---
# <a name="use-docker-with-a-jdk-for-azure"></a>Azure를 위해 JDK와 함께 Docker 사용 

이미 빌드된 Java 7, 8 및 11용 Docker 이미지는 [Docker Hub](https://hub.docker.com/_/microsoft-java-se)를 통해 사용할 수 있습니다.

여러 기본 OS 이미지의 Zulu JDK, JRE 및 JRE 헤드리스에 대해 인증된 Docker 컨테이너 이미지를 Docker Hub에서 사용할 수 있습니다.

* [JDK](https://hub.docker.com/_/microsoft-java-jdk)
* [JRE](https://hub.docker.com/_/microsoft-java-jre)
* [JRE 헤드리스](https://hub.docker.com/_/microsoft-java-jre-headless)

## <a name="running-a-docker-image"></a>Docker 이미지 실행

다음 예제와 같은 구문 `$ docker run mcr.microsoft.com/java/jdk:tag java`를 사용하여 Docker 이미지를 실행할 수 있습니다.

```cli
docker run mcr.microsoft.com/java/jdk:8u212-zulu-alpine java -version 
```

## <a name="creating-a-docker-image"></a>Docker 이미지 만들기

다음 예제와 같이 Microsoft의 공식 Docker Hub 이미지를 사용하여 이미지를 만들 수 있습니다.

### <a name="create-a-docker-file"></a>Docker 파일 만들기

```cli
FROM mcr.microsoft.com/java/jdk:8u212-zulu-alpine 
  
RUN echo $' \
  
public class HelloWorld { \
   public static void main(String[] args) { \
      // Prints "Hello, World" in the terminal window. \
      System.out.println("Hello, World - From Microsoft Azure !!!"); \
   } \
}' > HelloWorld.java
  
RUN javac HelloWorld.java
  
CMD ["java", "HelloWorld"]
```

### <a name="build-a-docker-image"></a>Docker 이미지 빌드

```cli
docker build -t hello-world
```

### <a name="run-the-new-image"></a>새 이미지 실행

```cli
docker run hello-world
```

다음 출력이 표시됩니다.

```output
Hello World - From Microsoft Azure !!!
```
