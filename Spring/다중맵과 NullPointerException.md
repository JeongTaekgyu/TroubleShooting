###NullPointerException 에러가 발생한 이유와 해결 방법

Request processing failed; nested exception is java.lang.NullPointerException

###원인

```java
public static boolean isLogined(Map<String, Object> mapParam)
{
	Map<String, Object> mapUser = getAdminKeyInfo(mapParam);
    ...
}
```

예를 들어 mapUser에 다음과 같은 값이 들어있을 때
{dpa_logininfo={userid=dtadmin, ref_usertype=100, username=admin}, dta_loginid=dtadmin}
안에 map이 두개? 들어있다

★그러므로★

```java
System.out.println("~~~: " + mapUser.get("ref_usertype").equals(100));
// 또는
if ( mapUser.get("ref_usertype").equals(100) ){...}
```

이런식으로 하면 NullPointerException 에러가 발생할 거다.



### 해결 방법

```java
if( ((Map<String, Object>)mapUser.get("dpa_logininfo")).get("ref_usertype").equals(100) )
```

이런식으로 해야 비교가 된다.

즉, sysout 안에 아래 처럼 출력가능

```java
((Map<String, Object>)mapUser.get("dpa_logininfo")).get("ref_usertype") 
```

바로 위 식을 아래처럼 두줄로 표현 가능

```java
Map<String, Object> tmp = (Map<String, Object<)mapUser.get("dpa_logininfo");
System.out.println(tmp.get("ref_usertype");
```

즉,

```java
String str = (String)map.get("string");
```

이랑 똑같다고 보면된다.