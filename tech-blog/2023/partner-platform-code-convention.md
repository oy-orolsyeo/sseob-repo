안녕하세요.

올리브영의 파트너들을 위한 서비스를 제공하는 파트너플랫폼 스쿼드 백엔드 개발자 🌼 들국화입니다.  

2023년 1 ~ 3분기에는 파트너오피스 서비스를 개선하는 작업들을 진행했는데요 !  

그 과정에서 스쿼드 구성원들끼리 약속한 코드 컨벤션을 소개해 드리려고 합니다 😚  

이 글에서는 코드 컨벤션의 개념, 중요성, 그리고 파트너플랫폼 구성원들이 세운 몇 가지 주요 원칙에 대해 알아보겠습니다.

# 코드 컨벤션이란 ?

코드 컨벤션은 개발 팀이 프로그램을 작성하고 유지보수하는 데 사용하는 일련의 규칙과 가이드라인을 의미합니다.

# 코드 컨벤션의 중요성 !

1️⃣ 가독성 향상  
> 코드 컨벤션을 따르면 모든 개발자들이 일관된 방식으로 코드를 작성하게 되어 코드베이스가 보다 읽기 쉽고 이해하기 쉬워집니다.  
> 이는 새로운 팀 멤버가 프로젝트에 참여하거나, 기존 코드를 다시 방문할 때 특히 중요합니다.


2️⃣ 유지보수성 향상  
> 팀 내에서 동일한 규칙을 공유하면 버그를 더 빨리 발견하고 수정할 수 있습니다.  
> 또한, 유지보수할 때 새로운 기능을 추가하거나 수정할 때 발생할 수 있는 충돌을 방지할 수 있습니다.  
> 다른 사람이 작성한 코드이더라도 동일한 규칙의 코드로 작성되어 있기 때문에 비교적 쉽게 수정할 수 있습니다.

3️⃣ 팀 협업 강화  
> 일관된 코드 스타일은 팀 내에서 원활한 협업을 가능하게 합니다.  
> 각 팀 멤버가 다양한 스타일을 사용하면 혼돈이 생길 수 있고, 팀 간의 소통이 어려워집니다.

# 파트너플랫폼 스쿼드의 주요 코드 컨벤션

1️⃣ 편집 설정

> Intellij IDEA와 같은 IDE를 사용하는 경우 탭 사이즈, 들여쓰기 사이즈, 인코딩 등을 간단하게 설정파일로 관리할 수 있습니다.  
> Intellij IDEA의 경우 .editorconfig 파일에 위 설정들을 기술하여 일관성 있게 관리할 수 있습니다.  
> 전체파일에 대한 공통 설정, java, yaml, groovy, bash, properties 등 파일별로도 설정할 수 있습니다.

![[editor-config.png]](./img/editor-config.png)

2️⃣ 패키지 구조

> 일관된 패키지 구조를 설계함으로서 서비스가 확장되더라도 명확한 구조를 갖게 합니다.  
> 새로운 모듈이나 기능이 추가될 때 기존의 구조에 맞춰 적절한 위치에 통합하기 쉽습니다.

![[package.png]](./img/package.png)

|package|기술 가이드|
|:---:|---|
| application | DTO, Application 로직을 담당하며, 주로 Service layer 클래스들을 정의합니다. |
|   domain    | 업무별로 잘 정의한 업무 도메인 관련 클래스들이 포함된 package 입니다. <br> 도메인 데이터를 저장하기 위한 DomainRepository, DomainService 등을 정의합니다. <br> DomainRepository의 경우 특정 저장소 (Database, File, API 등) 에 종속되지 않게 설계하기 위하여 추상화된 Interface로 설계하도록 합니다. |
|    infra    |저장소에 Access하는 구현체들을 작성합니다. <br> 추상화된 DomainRepository를 구현하도록 하며, DB, File, API 등 에서 데이터를 읽거나 쓸 수 있도록 설계합니다.|
|      ui     |외부로부터 들어온 Request를 routing처리하는 RestController를 정의합니다.|


3️⃣ 명명 규칙

> 변수, 메서드, 클래스 등에 일관된 명명 규칙을 적용해야 합니다.  
> 명확하고 의미 있는 이름을 사용하면 코드를 읽기 쉽게 만듭니다.

> User라는 Resource로 예시 가이드 작성.  

|행위|Controller and Service|Repository|
|:---:|:---:|:---:|
|자원 조회|getUser|findByUser <br> countByUser <br> existsByUser |
|자원 생성|createUser|insertUser|
|자원 삭제|removeUser|deleteUser|
|자원 수정|modifyUser|updateUser|
|Event 발행|UserEvent|-|

4️⃣ URI Design, HTTP Method

> 일관된 URI 구조는 새로운 Endpoint를 추가하거나, 기존 Endpoint를 수정하기 쉽게 합니다.  
> 통상적으로 사용되는 HTTP API 규칙을 적용하여, Client API가 서비스를 조금 더 쉽게 사용할 수 있습니다.

1. URI 설계시 자원은 단수 명사로 설계한다.  
2. 다수의 Resource를 생성, 수정, 삭제 등을 다루는 API는 URI에 bulk 라는 단어를 넣어 복수처리가 가능한 API임을 명시한다.
    ```json

    // POST partner-office/vendor/bulk

    {
        "vendors" : [
            {
                "vendorName" : "엘오케이",
                "phoneNumber" : "010-2586-3863",
                "email" : "orolsyeo@cj.net",
                "address" : "한강대로 372 19층"
            },
            {
                "vendorName" : "식물나라",
                "phoneNumber" : "010-2586-3863",
                "email" : "plantnara@cj.net",
                "address" : "을지로 3가"
            }
        ]
    }
    ```
3. Http method를 적극 활용하여 Resource를 다룬다.
    |행위|Http method|
    |:---|:---|
    |검색| GET |
    |생성| POST |
    |전체수정 or 생성| PUT |
    |일부 수정| PATCH|
    |삭제| DELETE |

5️⃣ Response 응답코드

> 일관성 : 응답 코드 패턴을 정의하면 Client는 서버 응답을 더 쉽게 이해하고 해석할 수 있습니다.  
> 오류 처리 단순화 가능 : 일관된 응답 코드 패턴을 사용하면 Client는 서버 응답을 쉽게 처리할 수 있습니다.
> 더 쉬운 문서화 : 응답 코드에 대한 컨벤션을 정립하면 API 문서 작성 작업을 더 단순하게 만듭니다.

> 응답코드 표

|예외 종류|정의|응답 상태 코드|내부 응답 코드|
|:---:|:---:|:---:|:---:|
|Success|성공|200|-|
|NoHandlerFound Exception|Endpoint를 찾을 수 없음|404|404|
|Server Exception|표준화된 서버 예외|500|500|
|Business Exception|업무/정책/검증 구현 예외|400|4xxx|
|Interlock Exception|외부 서비스 연동과 관련된 예외|500|I9xxx, R9xxx, C4xxx|
|Authentication Exception|인증 예외|401|1xxx|
|AccessDenied Exception|인가 예외|403|1xxx|
|Service Exception	|서비스 예외|500|500|
|Exception|최상위 예외|500|500|
|RequestLimit Exception	|API 호출 허용량 초과|429|(추가예정)|
|ServiceUnavailable Exception	|서버 점검|503|(추가예정)|

6️⃣ Resource에 대한 Response 메세지 규칙

1. 목록(Collection) 데이터를 Response할 때에는 같은 클래스를 사용한다.  
목록 데이터를 Generic하게 처리 가능한 클래스를 사용하여 응답 메세지 형태를 일관성있게 유지한다.

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

2. 특정 Resource를 다룰 때 응답 메세지 규칙

|행위|단건|여러 건|
|:---:|:---:|:---:|
|저장|저장된 identifier 를 반환|복수 identifier 를 반환|
|수정|수정된 identifier 를 반환|복수 identifier 를 반환|
|삭제|삭제된 identifier 를 반환|복수 identifier 를 반환|
|기타|identifier 가 없는 요청인 경우 Response Status 200을 응답하도록 합니다.|-|

<br>


# 마무리

코드 컨벤션은 팀의 효율성을 향상시키고 프로젝트의 성공을 돕는 핵심적인 부분입니다.  

스쿼드 구성원들이 일관된 스타일과 규칙을 준수하면 코드의 가독성과 유지보수성이 향상되어 좋은 개발 경험을 제공할 것입니다.

파트너플랫폼 스쿼드의 경우 코드 컨벤션을 모두 같이 정의하고, 시험하고, 재정의하고, 의견을 나누는 과정에서 많은 시간과 노력이 들었지만, 코드 컨벤션의 세워진 뒤로는 작업속도와 코드 품질, 코드를 이해하는 수준이 맞춰져 협업하는데 큰 도움이 되었습니다 😚

파트너플랫픔 스쿼드의 코드 컨벤션은 지금도 논의되며, 정의되고 있습니다.

읽어주셔서 감사합니다.