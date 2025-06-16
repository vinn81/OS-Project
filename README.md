# OS-Project
# Automatch - 풋살 매치 예약 및 자동 팀 배정 시스템

## 📌 1. 프로젝트 개요
사용자가 풋살 매치를 예약하고 자동으로 팀 배정을 해주는 웹 기반 시스템입니다.  
Spring Boot, JPA, MySQL, Thymeleaf 기반으로 개발되었습니다.

## ✅ 주요 기능
- 회원가입 및 로그인 (권한: **회원 / 매니저 / 관리자**)
- 회원: 매치 신청, 확인, 평가
- 매니저: 참가 인원 12명 이상 시 경기장 승인 요청 가능
- 관리자: 전체 회원/매치 정보 조회 및 승인

※ 로그인 시 자동으로 역할 구분

---

## ⚙️ 2. 실행 환경
- 운영체제: Windows 10 이상
- Java: **JDK 17 이상**
- Gradle: **7.x 이상** (Wrapper 포함)
- MySQL: **8.x** (3306 포트 기준)
- IDE: IntelliJ 권장

---

## 🛠️ 3. 데이터베이스 설정

MySQL 8.x 버전 설치 필요
다운로드: https://dev.mysql.com/downloads/mysql/

1) MySQL 실행 후 아래 SQL 실행:

CREATE DATABASE automatch DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

CREATE USER 'automatch_user'@'localhost' IDENTIFIED BY 'password';

GRANT ALL PRIVILEGES ON automatch.* TO 'automatch_user'@'localhost';

FLUSH PRIVILEGES;

2) 설정 파일 확인
src/main/resources/application.properties

spring.application.name=Automatch

spring.datasource.url=jdbc:mysql://localhost:3306/automatch
spring.datasource.username=automatch_user
spring.datasource.password=password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

spring.jpa.hibernate.ddl-auto=create
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect

4. JAR 파일 생성
plugins {
	id 'java'
	id 'org.springframework.boot' version '3.4.5'
	id 'io.spring.dependency-management' version '1.1.7'
}

group = 'com.example'
version = '0.0.1-SNAPSHOT'

java {
	toolchain {
		languageVersion = JavaLanguageVersion.of(17)
	}
}

repositories {
	mavenCentral()
}

dependencies {
	implementation 'com.h2database:h2'
	implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
	implementation 'org.springframework.boot:spring-boot-starter-security'
	implementation 'org.springframework.boot:spring-boot-starter-thymeleaf'
	implementation 'org.springframework.boot:spring-boot-starter-web'
	implementation 'org.thymeleaf.extras:thymeleaf-extras-springsecurity6'
	testImplementation 'org.springframework.boot:spring-boot-starter-test'
	testImplementation 'org.springframework.security:spring-security-test'
	testRuntimeOnly 'org.junit.platform:junit-platform-launcher'
}
tasks.named('test') {
	useJUnitPlatform()
}

5. 실행 방법
	1. 프로젝트 루트 디렉토리로 이동
	터미널 또는 명령 프롬프트를 엽니다.

	Automatch.zip을 압축 해제한 프로젝트 루트 폴더로 이동합니다.
	cd /경로/Automatch
	(예: Windows에서는 cd C:\Users\Username\Downloads\Automatch)

	2. JAR 파일 생성
	다음 명령어를 실행하여 JAR 파일을 생성합니다:
	./gradlew clean build
	💡 Windows에서는 gradlew.bat 사용 가능:
	gradlew.bat clean build
	빌드가 완료되면, 다음 경로에 JAR 파일이 생성됩니다:
	build/libs/automatch-0.0.1-SNAPSHOT.jar

	3. JAR 파일 실행
	터미널(명령 프롬프트)에서 JAR 파일이 있는 디렉토리로 이동합니다:
	cd build/libs
	아래 명령어를 사용하여 애플리케이션을 실행합니다:
	java -jar automatch-0.0.1-SNAPSHOT.jar

	4. 실행 결과 확인
	애플리케이션이 정상적으로 실행되면 다음과 유사한 메시지가 출력됩니다:
	Started AutomatchApplication in 4.321 seconds (JVM running for 4.789)

	5. 웹 브라우저 접속
	브라우저를 열고 아래 주소로 접속합니다:
	http://localhost:8080

권한별 기능
🧑‍🤝‍🧑 회원(Member)
매치 목록 확인

새 매치 신청

참가 매치 팀원 평가

🧑‍💼 매니저(Manager)
참가 인원 12명 이상인 경우 경기 승인 요청

ID: manager1

PW: pass1234

👨‍💼 관리자(Admin)
전체 회원 및 매치 정보 확인

매니저 승인 요청 수락

ID: admin

PW: admin123
