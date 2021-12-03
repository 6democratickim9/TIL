![image-20211125104318674](C:\Users\MIN\TIL\Spring\KOSTA_1125.assets\image-20211125104318674.png)

```xml
	<select id="findProductListLessThanPrice" parameterType="int"
		resultType="ProductVO">
		<include refid="selectProduct" />
		
		<![CDATA[
		where price <#{value}
		]]></select>
```

- `<![CDATA[where price <#{value}]]></select>`
  - CDATA Section: 해당 영역은 tag가 아니라 Character Data임을 알린다



- JOIN SQL: 하나 이상의 테이블을 결합하여 조회
- INNER JOIN: 조인 조건에 부합되는 정보를 조회
- OUTER JOIN: 조인 조건에 부합되지 않는 정보까지 모두 조회
- SELF JOIN: 하나의 테이블 자체에서 조회

