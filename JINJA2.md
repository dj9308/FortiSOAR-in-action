# JINJA 정리



## 정의

- jinja2 필터는 한 종류의 데이터를 정해진 정규식을 이용해서 추출하거나 변형시키는 방법 중 하나이다.
- {{Variable | Filter}} format이며, Filter 형식으로 Variable의 내용을 추출하거나 변형한다.
- 필터는 데이터의 모양이나 형식을 변형 시킬 수 있다.
- 필터는 같이 연동될 수 있으며 파이프에 의해 분리될 수 있다.
- 이 장점으로 인해 커스텀 필터를 사용할 수 있다.



## Function

**urlsplit()** 

- url을 fragment, hostname 등 여러 요소로 나눠서 표현하는 함수.

- ```jinja2
  {{ http://user:password@www.acme.com:9000/dir/index.html?query=termframent | urlsplit()}}
  
  object		{9}
  fragment	:	
  hostname	:	www.acme.com
  netloc	:	user:password@www.acme.com:9000
  password	:	password
  path	:	/dir/index.html
  port	:	9000
  query	:	query=termframent
  scheme	:	http
  username	:	user
  
  {{ http://user:password@www.acme.com:9000/dir/index.html?query=termframent | urlsplit('port')}}
  9000
  ```

**fromIRI**

- IRI를 확인하고 그 안에 있는 객체를 반환하며, 이는 ID로 객체와 유사하다.

- ```jinja2
  {{(vars.person_iri | fromIRI).name}}
  ->  개인 레코드를 검색하고 이름 필드를 반환.
  {{((vars.event.alert | fromIRI).owner | fromIRI)}}
  -> 재귀적 함수 사용
  {{('/api/3/alerts/<alert_IRI>?$relationships=true' | fromIRI).indicators}}
  -> 플레이북이 실행 중인 레코드에 대한 관계 데이터 검색
  ```

**json2html**

- json 데이터를 row_fields html로 변환시킨다.

- ```jinja2
  {{[{"pid": 123, "sid": "123", "path":"abc.txt"}] | json2html }}
  -> <table class="cs-data-table"><tr> <th>pid</th> <th>sid</th> <th>path</th> </tr> <tr> <td>123</td> <td>123</td> <td>abc.txt</td> </tr> </table>
  {{[{"pid": 123, "sid": "123", "path":"abc.txt"}] | json2html(['pid','sid'])}}
  -> <table class="cs-data-table"><tr> <th>pid</th> <th>sid</th> </tr> <tr> <td>123</td> <td>123</td> </tr> </table>
  ```

**json_query**

- 가장 간단한 JMESPath 표현식은 JSON 객체에서 키를 선택하고 특정 값을 반환하는 식별자이다.

- ```jinja2
  {{vars.Address | json_query('[*]["name"]')}}
  ```

- 
