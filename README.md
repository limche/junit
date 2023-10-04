# JUnit 사용 가이드

## 목차:
1. [JUnit 5/Mockito](#junit-5mockito)
2. [Gradle 실행](#gradle-실행)
3. [JaCoCo Test Coverage](#jacoco-test-coverage)
4. [SonarQube 연동](#sonarqube-연동)

---

## 1. JUnit 5/Mockito

### JUnit 5 주요 기능

- **@Test**: 테스트 케이스를 선언합니다.
- **@BeforeEach / @AfterEach**: 각 테스트 케이스 실행 전/후에 수행할 작업을 선언합니다.
- **@BeforeAll / @AfterAll**: 모든 테스트 시작 전과 후에 한 번씩 실행됩니다.
- **@ParameterizedTest**: 다양한 입력값에 대해 같은 테스트 로직을 수행하고자 할 때 사용합니다.
- **@Disabled**: 일시적으로 테스트를 비활성화합니다.

### Mockito 주요 기능

- **mock()**: mock 객체를 생성합니다.
- **when() / thenReturn()**: mock 메서드의 반환 값을 설정합니다.
- **verify()**: mock 객체의 메서드 호출 여부와 횟수를 검증합니다.

---

## 2. Gradle 실행

프로젝트 빌드:
./gradlew build

테스트 실행:
./gradlew test

---

## 3. JaCoCo Test Coverage

### Gradle에 JaCoCo 설정하기

`build.gradle` 파일에 JaCoCo 플러그인을 추가하고, 필요한 설정을 정의합니다:

plugins {
    id 'jacoco'
}

jacoco {
    toolVersion = '0.8.7'  // 사용할 JaCoCo 버전을 지정합니다.
    reportsDir = file("$buildDir/customJacocoReportDir")
}

jacocoTestReport {
    reports {
        xml.enabled true
        csv.enabled false
        html.destination file("${buildDir}/jacocoHtml")
    }
}

## 4. SonarQube 연동

### Gradle에 SonarQube 설정하기

build.gradle 파일에 SonarQube 플러그인을 추가하고, 필요한 설정을 정의합니다:

plugins {
    id "org.sonarqube" version "3.3"  // 사용할 SonarQube 플러그인의 버전을 지정합니다.
}

sonarqube {
    properties {
        property "sonar.projectName", "Your Project Name"
        property "sonar.projectKey", "your-project-key"
        property "sonar.sourceEncoding", "UTF-8"
        property "sonar.sources", "src/main/java"
        property "sonar.tests", "src/test/java"
        property "sonar.java.coveragePlugin", "jacoco"
        property "sonar.jacoco.reportPaths", "$buildDir/jacoco/test.exec"
        // 필요한 경우 추가적인 SonarQube 속성을 정의할 수 있습니다.
    }
}
