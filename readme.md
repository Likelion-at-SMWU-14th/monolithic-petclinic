# Monolithic Pet Clinic — 숙명 멋사 14기 MSA 세미나

하나로 뭉쳐 있는 모놀리식 Pet Clinic을 **Strangler Fig Pattern**으로 조금씩 마이크로서비스로 분리해 보는 실습 레포지토리입니다.

> 원본: [gregorriegler/monolithic-petclinic](https://github.com/gregorriegler/monolithic-petclinic)
> 세미나용으로 **Gradle + Spring Boot 4 + Java 21** 기준으로 업그레이드했습니다.

## 준비물

- JDK 21 이상
- IntelliJ IDEA (Community도 OK)
- Git

## 실행하기

```bash
# macOS / Linux
./gradlew monolith:bootRun

# Windows
gradlew.bat monolith:bootRun
```

브라우저에서 확인해 보세요.

| 주소 | 내용 |
|---|---|
| http://localhost:8080 | Pet Clinic 메인 |
| http://localhost:8080/owners/find | 고객(Owner) 검색 |
| http://localhost:8080/vets | 수의사 목록 |
| http://localhost:8080/manage/health | 서버 상태 (Actuator) |

## 구조

```
monolithic-petclinic
├── monolith/          # 오늘 쪼갤 모놀리식 애플리케이션 (port 8080)
│   └── src/main/java/org/springframework/samples/petclinic
│       ├── controller/   # Owner, Pet, Visit, Vet, Management 화면
│       ├── service/      # ClinicService: 모든 도메인이 한 클래스에!
│       ├── db/           # Spring Data JPA Repository
│       └── model/        # Owner, Pet, Visit, Vet ...
├── build.gradle       # 모든 모듈 공통 설정
└── settings.gradle    # 모듈 목록 (실습에서 서비스를 하나씩 추가합니다)
```

## 실습 브랜치

| 브랜치 | 내용 |
|---|---|
| `main` | 시작점: 모놀리스만 있는 상태 |
| `step1-start` / `step1-done` | 실습1: Customer Service 분리 |
| `step2-start` / `step2-done` | 실습2: API Gateway 구축 |
| `step3-start` / `step3-done` | 실습3: 장애 실험 |

실습 중에 막히면 다음 단계의 `-done` 브랜치로 이동해서 따라오면 됩니다.

```bash
git checkout step1-done
```

## 데이터베이스

인메모리 HSQLDB를 사용합니다. 서버를 켤 때마다 `monolith/src/main/resources/db`의 `schema.sql`, `data.sql`로 초기화되므로, 서버를 껐다 켜면 추가한 데이터는 사라집니다.

## License

Apache License 2.0 (원본 Spring PetClinic과 동일)
