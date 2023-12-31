
안녕하세요 !

올리브영의 파트너들을 위한 서비스를 제공하는 파트너플랫폼 스쿼드 백엔드 개발자 🌼 들국화입니다.  

2023년 3 ~ 4분기에는 파트너오피스 서비스를 개선, 개발하는 작업들을 진행했는데요 !  

파트너오피스 서비스를 개선, 개발하는 과정에서 `레거시 코드들이 마음에 들지않는다`, `안티 패턴을 제거하자 !`, `앞으로는 이런 규칙으로 개발되었으면 좋겠다 !` 등등 많은 의견이 도출되었습니다.  

 그 의견들을 가지고 이야기를 나누고, 조사하고, 씨름하는 과정에서 구성원들이 약속한 코드 컨벤션 일부분을 소개해 드리려고 합니다. ☺️  

이 글에서는 코드 컨벤션의 개념, 중요성, 그리고 파트너플랫폼 구성원들이 세운 몇 가지 주요 원칙에 대해 알아보겠습니다.

# 코드 컨벤션이란 ?

코드 컨벤션은 개발팀이 프로그램을 작성하고 유지 보수하는 데 사용하는 일련의 규칙과 가이드라인을 의미합니다.

# 코드 컨벤션의 중요성 !

### 1️⃣ 가독성 향상  

코드 컨벤션을 따르면 모든 개발자들이 일관된 방식으로 코드를 작성하게 되어 코드베이스가 보다 읽기 쉽고 이해하기 쉬워집니다.  

이는 새로운 팀 멤버가 프로젝트에 참여하거나, 기존 코드를 다시 방문할 때 특히 중요합니다.

<br>

### 2️⃣ 유지 보수성 향상  

팀 내에서 동일한 규칙을 공유하면 버그를 더 빨리 발견하고 수정할 수 있습니다.  

또한, 유지 보수할 때 새로운 기능을 추가하거나 수정할 때 발생할 수 있는 충돌을 방지할 수 있습니다.  

다른 사람이 작성한 코드이더라도 동일한 규칙의 코드로 작성되어 있기 때문에 비교적 쉽게 수정할 수 있습니다.  

<br>

### 3️⃣ 팀 협업 강화  

일관된 코드 스타일은 팀 내에서 원활한 협업을 가능하게 합니다.  

각 팀 멤버가 다양한 스타일을 사용하면 혼돈이 생길 수 있고, 팀 간의 소통이 어려워집니다.

<br>

# 파트너플랫폼 스쿼드의 주요 코드 컨벤션

### 1️⃣ 편집 설정

Intellij IDEA와 같은 IDE를 사용하는 경우 탭 사이즈, 들여쓰기 사이즈, 인코딩 등을 간단하게 설정파일로 관리할 수 있습니다.  

Intellij IDEA의 경우 .editorconfig 파일에 위 설정들을 기술하여 일관성 있게 관리할 수 있습니다.  

전체파일에 대한 공통 설정, java, yaml, groovy, bash, properties 등 파일별로도 설정할 수 있습니다.

![[editor-config.png]](./img/editor-config.png)

<br>

### 2️⃣ 패키지 구조

일관된 패키지 구조를 설계함으로써 서비스가 확장되더라도 명확한 구조를 갖게 합니다.  

새로운 모듈이나 기능이 추가될 때 기존의 구조에 맞춰 적절한 위치에 통합하기 쉽습니다.  

패키지 구조에 대한 컨벤션을 정의할 때 가장 신경 쓴 부분은 의존성의 분리, 도메인과 비즈니스의 분리입니다.  

```
.
├── java
│   └── com
│       └── example
│           └── demo
│               ├── DemoApplication.java
│               └── member
│                   ├── application
│                   │   ├── MemberService.java
│                   │   └── dto
│                   │       └── MemberSearch.java
│                   ├── domain
│                   │   └── MemberRepository.java
│                   ├── infra
│                   │   ├── MemberMapper.java
│                   │   └── MemberRepositoryImpl.java
│                   └── ui
│                       └── MemberController.java
│


```

✅ **패키지 구조에 따른 기술 가이드**


![[package-table.png]](./img/package-table.png)

<br>

### 3️⃣ 명명 규칙

변수, 메서드, 클래스 등에 일관된 명명 규칙을 적용해야 합니다.  

명확하고 의미 있는 이름을 사용하면 코드를 읽기 쉽게 만듭니다.  

변수, 메서드, 클래스의 명칭은 의미를 알 수 없는 축약어를 사용하지 않고, 되도록이면 풀어서 작성하도록 합니다.  

<br>

✅ **Layer별 메서드 명칭 예시 가이드.**

![[naming-table.png]](./img/naming-table.png)

Controller ~ Service Layer의 메서드 명칭과 Repository Layer의 메서드 명칭을 다르게 작성하여,  

비즈니스 로직이 동작하는 메서드인지, 저장소에 Accesss 하기위한 기능을 제공하는 메서드인지 구별할 수 있도록 합니다.

<br>
<br>

### 4️⃣ URI Design, HTTP Method

일관된 URI 구조는 새로운 Endpoint를 추가하거나, 기존 Endpoint를 수정하기 쉽게 합니다.  

통상적으로 사용되는 HTTP API 규칙을 적용하여, Client API가 서비스를 더 쉽게 사용할 수 있습니다.  

<br>

1. URI 설계할 때 자원은 단수 명사로 설계한다.

<br>

2. 다수의 Resource를 생성, 수정, 삭제 등을 다루는 API는 URI에 bulk 라는 단어를 넣어 복수처리가 가능한 API임을 명시한다.
    ```json

    // POST partner-office/vendor/bulk

    {
        "vendors" : [
            {
                "vendorName" : "엘오케이",
                "phoneNumber" : "010-****-****",
                "email" : "orolsyeo@cj.net",
                "address" : "한강대로 372 19층"
            },
            {
                "vendorName" : "식물나라",
                "phoneNumber" : "010-****-****",
                "email" : "plantnara@cj.net",
                "address" : "을지로 3가"
            }
        ]
    }
    ```
3. Http method를 적극 활용하여 Resource를 다룬다.
   ![[http-method-table.png]](./img/http-method-table.png "Http method 표")


### 5️⃣ Response 응답 코드

일관성 : 응답 코드 패턴을 정의하면 Client는 서버 응답을 더 쉽게 이해하고 해석할 수 있습니다.  

오류 처리 단순화 가능 : 일관된 응답 코드 패턴을 사용하면 Client는 서버 응답을 쉽게 처리할 수 있습니다.  

더 쉬운 문서화 : 응답 코드에 대한 컨벤션을 정립하면 API 문서 작성 작업을 더 단순하게 만듭니다.

<br>

✅ **응답 코드 표**
![[exception-table.png]](./img/exception-table.png "응답코드 표")


### 6️⃣ Resource에 대한 Response 메세지 규칙

1. **목록(Collection) 데이터를 Response할 때에는 같은 클래스를 사용합니다.**  

    목록 데이터를 Generic하게 처리 가능한 클래스를 사용하여 응답 메세지 형태를 일관성 있게 유지합니다.  

    `data` field의 내부 값은 다양한 형태의 값을 다룰 수 있도록 Gerneric type의 목록 데이터 타입으로 만들었고, `totalCount`, `page`, `pageSize`, `summary` field는 일관성 있게 항상 응답할 수 있도록 합니다.  

    Client는 일관성 있게 목록 데이터를 처리할 수 있습니다.

    ```java
   
    @Getter
    @JsonInclude(JsonInclude.Include.NON_NULL)
    public class RestCollectionResponse<T> {

        private final List<T> data;
    
        private Long totalCount;
    
        private Integer page;
    
        private Integer pageSize;
    
        private T summary;
   
    }
    ```

2. **단일 Resource를 다룰 때 응답 메세지 규칙**

    응답 메세지 형태를 일관성 있게 유지합니다.

    저장, 수정, 삭제 시 identifier를 Client에 일관성 있게 항상 응답할 수 있도록 합니다.  

    Client는 Http Status 뿐만 아니라, identifier를 활용하여 응답이 성공되었음을 확인할 수 있습니다.  

    Client는 응답받은 identifier를 통해 요청 이후 후처리를 할 수 있습니다.

    ![[response-message-table.png]](./img/response-message-table.png "응답 메세지 표")

<br>


# 마무리

코드 컨벤션은 팀의 효율성을 향상시키고 프로젝트의 성공을 돕는 핵심적인 부분입니다.  

스쿼드 구성원들이 일관된 스타일과 규칙을 준수하면 코드의 가독성과 유지 보수성이 향상되어 좋은 개발 경험을 제공할 것입니다.

파트너플랫폼 스쿼드의 경우 코드 컨벤션을 모두 같이 정의하고, 시험하고, 재정의하고, 의견을 나누는 과정에서 많은 시간과 노력이 들었지만,   

코드 컨벤션이 세워진 뒤로는 작업속도와 코드 품질, 코드를 이해하는 수준이 맞춰져 협업하는 데 큰 도움이 되었습니다 ☺️

파트너플랫픔 스쿼드의 코드 컨벤션은 지금도 논의되며, 정의되고 있습니다.

읽어주셔서 감사합니다.