# Spring Cloud Config 삽질과 정리

### 나의 삽질이 담긴 깃 주소....
- 값을 읽어다 주는 API가 있는 repo
    - https://github.com/sang5c/spring-cloud-config
- 실제 설정이 담긴 주소
    - https://github.com/sang5c/spring-config-repository

---

## 삽질의 원인
방심했다. 항상 글을 제대로 읽고 천천히 따라하자.

로컬에다 만들고 Repository에서 읽도록 설정해서 고생을 많이했다.


## Spring Cloud Config를 사용하는 방법 두가지
1. API서버를 만들고 설정 파일을 추가한 후 설정 파일을 로컬에서 읽기
2. 설정 파일이 담긴 Repository를 만들고 이를 읽어오는 방법

.yml, .properties 둘다 가능하다.


### 1. 로컬에서 읽기 
~~얜 안돌려봤음... 이게 맞나?~~

로컬에서 읽기 위해서는 스프링 프로필을 native로 설정해줘야 한다.
~~~
spring:
  cloud:
     config:
       server:
         native:
           search-locations: classpath:/config,classpath:config/test  # classpath의 config/, config/test/ 폴더에서 읽는다. 
~~~ 
~~주의(?) !
docs에는 searchLocations 라고 나오지만 IDEA Ultimate에서 자동완성은 search-locations 라고 되는...?~~

해보니까 searchLocations와 search-locations 둘다 작동한다. 코딩스타일을 지키기 위한 배려.....?

### 2. git Repository에서 읽기
~~~
spring:
  cloud:
     config:
       server:
         git:
           uri: https://github.com/sang5c/spring-config-repository
~~~


TODO: config 

#### 참조 (정리 엄청 잘됨)
- http://blog.leekyoungil.com/?p=352
- https://github.com/gilbutITbook/006962/blob/master/spmia-chapter3/confsvr/src/main/resources/application.yml
- https://brunch.co.kr/@springboot/113
- https://spring.io/projects/spring-cloud-config
- https://luvstudy.tistory.com/63
