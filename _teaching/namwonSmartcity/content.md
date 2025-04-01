---
title: "남원 통합플랫폼 개발 회고록"
collection: teaching
type: "webEvent"
permalink: /teaching/namwonSmartcity/content
venue: "직장"
date: 2025-04-01
---

# 남원 통합플랫폼 회고록

---
## 개요
- 남원 통합플랫폼 개발을 진행하면서 겪은 차이점과 느낀점을 정리한 회고록

---
## 개발환경
- 개발언어: Java, JavaScript , spring
- 데이터베이스: PostgreSQL
- 서버: Apache Tomcat
- 형상관리: SVN
- 기타: Jira, Confluence
- 개발기간: 2024.04 ~ 2025.04
---

## 차이점
- 차이점1: 기존 형상관리와 다른 형상관리 사용
  - 기존은 형상관리로 git을 사용하고 있었는데 새로운 프로젝트에서는 SVN을 사용하고 있었음
  - 이로 인해 git을 사용하던 개발자들은 SVN을 사용하는데 어려움을 겪음
- 사용: SVN 사용법을 학습하여 사용
- 참조 : https://goddaehee.tistory.com/196
- 느낀점 : 형상관리는 프로젝트의 성패를 좌우하는 중요한 요소이므로 개발자들이 익숙한 형상관리를 사용하는 것이 좋다고 생각함

---

- 차이점2: 기존 프로젝트와 다른 mybatis 설정
  - datasource 설정
  - 기존은 org.apache.commons.dbcp.BasicDataSource를 사용하고 있었음
  - 새로운 프로젝트에서는 org.apache.ibatis.datasource.pooled.PooledDataSource를 사용하고 있음
  ```xml
  <!-- 기존 -->
  <bean id="dataSource" class="org.apache.ibatis.datasource.pooled.PooledDataSource"></bean>
  <!-- 신규 -->
  <bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close"></bean>
  ```
  - 실무에서는 보통 BasicDataSource나 HikariCP 같은 전문적인 커넥션 풀 라이브러리를 사용하는 것이 권장됨
  - 느낀점 : mybatis 설정은 프로젝트의 성능에 영향을 미치므로 신중하게 설정해야함
  
  - sqlsessionbean 설정
  ```xml
  <!-- 기존 -->
  <bean id="sqlSessionFactory" class="com.daehoeng.cloud.common.mybatis.RefreshableSqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource" />
        <property name="configLocation" value="classpath:mybatis-config.xml" />
        <property name="mapperLocations" value="classpath:/**/maps/**/*.xml" />
        <property name="interval" value="1000" />
  </bean>
  
   <!-- 신규 -->
  <bean id="sqlSession" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource" />
        <property name="configLocation"  value="classpath:/geomex/xeus/setting/mybatis/config.xml" />
        <property name="mapperLocations" value="classpath:/geomex/xeus/setting/mappers/*.xml" />
  </bean>
  ```
  - 느낀점 : RefreshableSqlSessionFactoryBean은 표준 SqlSessionFactoryBean을 확장한 것으로, 주로 개발 시 편의성을 위해 매퍼 파일의 동적 리로드 기능을 제공
  - 기존 프로젝트에서는 mapper 파일을 수정하면 서버를 재시작하지 않아도 즉시 반영되는 장점이 있었음
  - 신규 프로젝트에서는 mapper 파일을 수정하면 서버를 재시작해야만 반영되는 단점이 있었음
  
  - mybatis 설정
  ```xml
  <!-- 기존 -->
  <!-- mybatis-config.xml -->
  <configuration>
    <settings>
       <!-- NULL 값을 데이터베이스에 전달할 때 JDBC NULL 타입으로 처리 -->
       <setting name="jdbcTypeForNull" value="NULL" />
       
       <!-- MyBatis 캐시 기능 활성화 - SQL 쿼리 결과를 캐싱하여 성능 향상 -->
       <setting name="cacheEnabled" value="true" />
       
       <!-- 지연 로딩(Lazy Loading) 비활성화 - 연관 객체들을 즉시 로딩 -->
       <setting name="lazyLoadingEnabled" value="false" />
       
       <!-- 단일 쿼리로 여러 결과셋 반환 허용 -->
       <setting name="multipleResultSetsEnabled" value="true" />
       
       <!-- 결과셋에서 컬럼 이름 대신 컬럼 라벨 사용 -->
       <setting name="useColumnLabel" value="true" />
       
       <!-- 자동 생성 키(auto-generated keys) 기능 비활성화 -->
       <setting name="useGeneratedKeys" value="false" />
       
       <!-- SQL 실행기 타입을 REUSE로 설정 - PreparedStatement 재사용으로 성능 최적화 -->
       <setting name="defaultExecutorType" value="REUSE" />
       
       <!-- 데이터베이스 컬럼의 언더스코어 명명법을 Java 객체의 카멜케이스로 자동 변환 (예: user_name → userName) -->
       <setting name="mapUnderscoreToCamelCase" value="true" />
    </settings>

    <mappers>
       <!-- 페이징 처리 관련 공통 SQL 매퍼 파일 등록 -->
       <mapper resource="mybatis/Page.xml" />
    </mappers>  
  </configuration>
  <!-- 신규 -->
  <!-- config.xml -->
  <configuration>
    <settings>
        <!-- 데이터베이스 컬럼명의 언더스코어 표기법을 Java 객체의 카멜케이스 속성명으로 자동 변환
             (예: user_name → userName, patrol_id → patrolId) -->
        <setting name="mapUnderscoreToCamelCase" value="true"/>
    </settings>
    
    <typeAliases>
        <!-- PatrolVo 클래스에 대한 별칭 설정
             전체 패키지 경로(geomex.xeus.equipmgr.service.PatrolVo) 대신 
             'PatrolVo'라는 짧은 이름으로 매퍼 XML에서 사용 가능 -->
        <typeAlias type="geomex.xeus.equipmgr.service.PatrolVo" alias="PatrolVo"/>
    </typeAliases>
  </configuration>
  ```
  - 공통점 : mapUnderscoreToCamelCase 설정을 두 프로젝트 다 true로 설정하여 데이터베이스 컬럼명과 Java 객체 속성명 간의 매핑을 수동으로 작성할 필요가 없어짐
  - 차이점 : typeAliases 설정이 기존 프로젝트에서는 없었음
  - 느낀점 : typeAliases 설정을 통해 별칭을 설정하면 매퍼 XML에서 클래스의 전체 패키지 경로를 사용하지 않고 짧은 이름으로 사용할 수 있어 편리함

  - page.xml 설정
  ```xml
  <!-- 기존 -->
  <!-- page.xml 로 분리되어있음-->
  <mapper namespace="Page">
	<sql id="Top">
		SELECT ROW_NUMBER() OVER(
			<if test="sorts != null and !sorts.isEmpty and sorts.size() > 0">
				ORDER BY
				<foreach collection="sorts" item="item" index="index" open="" separator=", "  close="">
					A.${item.column} ${item.type}
				</foreach>
			</if>
			) AS RNUM, A.*
				FROM (
	</sql>

	<sql id="Bottom">
		) AS A
		<if test="isPaging">
			LIMIT #{length} OFFSET #{start}
		</if>
	</sql>

	<sql id="Search">
		<if test="searchType != null and searchType != '' and searchWrod != null and searchWrod != ''">
			AND "${searchType}" LIKE CONCAT('%', #{searchWord}, '%')
		</if>
		<if test="searchDateColumn != null and searchDateColumn != '' and searchStartDate != null">
			AND ${searchDateColumn} &gt;= TO_DATE(#{searchStartDate}, 'yyyy-MM-dd')
		</if>
		<if test="searchDateColumn != null and searchDateColumn != '' and searchEndDate != null">
			AND ${searchDateColumn} &lt; TO_DATE(#{searchEndDate}, 'yyyy-MM-dd') + 1
		</if>
	</sql>
  </mapper>
  
  <!-- 신규 -->
  <!-- 모든 xml 마다 작성해야함 -->
  <where>
      <if test="emdCd != null and emdCd != ''">
          AND emd.emd_cd = #{emdCd}
      </if>
      <if test="name != null and name != ''">
          AND xaa.name LIKE '%' || #{name} || '%'
      </if>
      <if test="searchInput != null and searchInput != ''">
          AND xaa.name LIKE '%' || #{searchInput} || '%'
      </if>
      <if test="state != null and state != ''">
          AND (
          (#{state} = 'Y' AND xaa.status LIKE '%정상%') OR
          (#{state} = 'N' AND xaa.status NOT LIKE '%정상%')
          )
      </if>
  </where>

  <trim prefix="ORDER BY">
      <if test="sortCol != null and sortCol != '' and sortTyp != null and sortTyp != ''">
          ${sortCol} ${sortTyp}
      </if>
      <if test="sortCol == null and sortTyp == null">
          xaa.mgr_no asc
      </if>
  </trim>

  <if test="limit != null and limit != '' and offset != null and offset != ''">
      LIMIT ${limit} OFFSET ${offset}
  </if>
  ```
  - 공통점 : 페이징 처리 관련 공통 SQL 매퍼 파일을 등록하여 페이징 처리를 위한 SQL을 재사용
  - 차이점 : 기존 프로젝트에서는 Top, Bottom, Search SQL을 사용하고 있었음
  - 기존 프로젝트에서는 Top SQL에서 ROW_NUMBER() OVER() 함수를 사용하여 페이징 처리를 하고 있었음
  - 신규 프로젝트에서는 where, trim, if 태그를 사용하여 페이징 처리를 하고 있음
  - Top, Bottom, Search SQL을 사용하면 반복되는 태그를 간결하게 사용할 수 있음
---
    
  
  
