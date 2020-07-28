---
title: Maven vs Gradle
tags: markdown 
comments: true
---

Maven vs Gradle 

**목차**

- [[Maven::#maven]]
- [[Gradle::#gradle]]
- [[Maven vs Gradle::#vs]]

---

{:#maven}
### Maven

Apache의 이름 아래 2004년 출시

Ant를 사용하던 개발자들의 불편함을 해소 + 부가기능 추가

Maven은 무엇인가?

- 빌드를 쉽게 (Making the build process easy)
- pom.xml을 이용한 정형화된 빌드 시스템 (Providing a uniform build system)
- 뛰어난 프로젝트 정보 제공 (Providing quality project information_
	- 소스 제어에서 직접 작성된 변경 로그 문서
	- 상호 참조 소스
	- 메일 링리스트
	- 의존성 목록
	- 적용 범위를 포함한 단위 테스트 보고서
- 개발 가이드 라인 제공 (Providing guidelines for best practices development)
	- 테스트 소스 코드를 별도의 병렬 소스 트리에 유지
	-	테스트 케이스 이름 지정 규칙을 사용하여 테스트를 찾고 실행
	-	테스트 케이스에 환경을 설정하고 테스트 준비를위한 빌드 사용자 정의에 의존하지 마십시오.
새로운 기능을 쉽게 설치할 수 있고 업데이트할 수 있음 (Allowing transparent migration to new features)



---

{:#gradle}
### Gradle

Ant와 Maven의 장점을 모아모아 2012년 출시

Android OS의 빌드 도구로 채택 됨

#### Gradle이란 무엇인가?

	- Ant처럼 유연한 범용 빌드 도구 (A very flexible general purpose build tool like Ant.)
	- Maven을 사용할 수 있는 변환 가능 컨벤션 프레임 워크 (Switchable, build-by-convention frameworks a la Maven. But we never lock you in!)
	- 멀티 프로젝트에 사용하기 좋음 (Very powerful support for multi-project builds.)
	- Apache Ivy에 기반한 강력한 의존성 관리 (Very powerful dependency management (based on Apache Ivy))
	- Maven과 Ivy 레파지토리 완전 지원 (Full support for your existing Maven or Ivy repository infrastructure.)
	- 원격 저장소나, pom, ivy 파일 없이 연결되는 의존성 관리 지원
	(Support for transitive dependency management without the need for remote repositories or pom.xml and ivy.xml files.)
	- 그루비 문법 사용 (Groovy build scripts.)
	- 빌드를 설명하는 풍부한 도메인 모델 (A rich domain model for describing your build.)


---

{:#vs}

### Maven vs Gradle
Maven에는 gradle과 비교 문서가 없지만, gradle에는 비교문서가 존재.
Gradle이 시기적으로 늦게 나온만큼 사용성, 성능 등 비교적 뛰어난 스펙을 가지고있다.

#### Gradle이 Maven보다 좋은점

- Build라는 동적인 요소를 XML로 정의하기에는 어려운 부분이 많다.
	- 설정 내용이 길어지고 가독성 떨어짐
	- 의존관계가 복잡한 프로젝트 설정하기에 부적절
	- 상속구조를 이용한 멀티 모듈 구현
	- 특정 설정을 소수의 모듈에서 공유하기 위해서는 부모 프로젝트를 생성하여 상속하게 해야 함 (상속의 단점 생김)
- Gradle은 Groovy를 사용하기 때문에, 동적인 빌드는 Groovy 스크립트로 플러그인을 호출하거나 직접 코드를 짜면 된다.
	- Configuration Injection 방식을 사용해서 공통 모듈을 상속해서 사용하는 단점을 커버했다.
	- 설정 주입 시 프로젝트의 조건을 체크할 수 있어서 프로젝트별로 주입되는 설정을 다르게 할 수 있다.
 

#### 방법
	- Gradle을 데몬은 메모리에 빌드 정보 "핫"을 유지하는 수명이 긴 과정이다
	- 다양한 유형의 작업에 대한 증분 작업 입력 및 출력으로 인해 다시 깨끗하게 실행할 필요가 없습니다.
	- 증분 컴파일 은 소스와 클래스 간의 종속성을 분석하고 변경의 영향을받는 항목 만 다시 컴파일합니다.
	- 빌드 캐시는 지점 전환 또는 정리 빌드를 실행하고 동일한 출력이 이미 조직에서 다른 곳에서 생산 된 캐시의 결과를 가져옵니다.
	- Gradle의 스마트 클래스 경로 분석기 는 라이브러리의 바이너리 인터페이스가 변경되지 않은 경우 불필요한 컴파일을 피합니다.
	- Java 라이브러리 플러그인을 사용하여 종속성을 더 잘 모델링 하면 컴파일 클래스 경로의 크기가 줄어들어 성능에 큰 긍정적 영향을 미칩니다.


---

### 예시 비교

#### Maven
```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
   <modelVersion>4.0.0</modelVersion>

   <groupId>com.example</groupId>
   <artifactId>demo-maven</artifactId>
   <version>0.0.1-SNAPSHOT</version>
   <packaging>jar</packaging>

   <name>demo-maven</name>
   <description>Demo project for Spring Boot</description>

   <parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
      <version>1.5.4.RELEASE</version>
      <relativePath/> <!-- lookup parent from repository -->
   </parent>

   <properties>
      <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
      <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
      <java.version>1.8</java.version>
   </properties>

   <dependencies>
      <dependency>
         <groupId>org.springframework.boot</groupId>
         <artifactId>spring-boot-starter</artifactId>
      </dependency>

      <dependency>
         <groupId>org.springframework.boot</groupId>
         <artifactId>spring-boot-starter-test</artifactId>
         <scope>test</scope>
      </dependency>
   </dependencies>

   <build>
      <plugins>
         <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
         </plugin>
      </plugins>
   </build>


</project>
```

#### Gradle
```
buildscript {
    ext {
        springBootVersion = '1.5.4.RELEASE'
    }
    repositories {
        mavenCentral()
    }
    dependencies {
        classpath("org.springframework.boot:spring-boot-gradle-plugin:${springBootVersion}")
    }
}

apply plugin: 'java'
apply plugin: 'idea'
apply plugin: 'org.springframework.boot'

version = '0.0.1-SNAPSHOT'
sourceCompatibility = 1.8

repositories {
    mavenCentral()
}


dependencies {
    compile('org.springframework.boot:spring-boot-starter')
    testCompile('org.springframework.boot:spring-boot-starter-test')
}
```

---

### 결론
Ant의 유연한 구조적 장점과 Maven의 편리한 의존성 관리 기능을 합쳐놓은 것만으로도 많은 인기를 얻었던 Gradle은 버전이 올라가며 성능이라는 장점까지 더해지면서 대세가 되었다.

물론 그동안 사용해왔던 Maven과 이제는 익숙해진 XML을 버리고 Gradle과 Groovy문법을 배우는 것은 적지않은 비용이 든다.

특히 협업을 하는 경우, 프로젝트 구성과 빌드만을 위해 모든 팀원이 Groovy 문법을 익여야 한다는 사실은 Gradle를 사용하는데 큰 걸림돌이 된다.

실제로 여전히 Maven의 사용률은 Gradle을 앞서고 있으며 구글 트랜드 지수도 Maven이 Gradle을 앞선다.

협업과 러닝커브를 고려하여 여전이 Maven를 사용하는 팀이 많고 부족함 없이 잘 사용하고 있지만,

앞서 요약했듯 프로젝트의 빌드타임이 비용문제로 이어질 경우 Gradle을 사용해야 할 것 같다.

## 출처
-  https://bkim.tistory.com/13
- https://gradle.org/
- https://maven.apache.org/
- http://egloos.zum.com/kwon37xi/v/4747016
