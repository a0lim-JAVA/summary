## swagger
1. 의존성 추가
  - build.gradle에서 dependency 추가
    ```
    implementation 'io.springfox:springfox-boot-starter:3.0.0'
    implementation 'io.springfox:springfox-swagger-ui:3.0.0'
    implementation 'io.springfox:springfox-bean-validators:3.0.0'
    ```
  - swaggerConfig 파일 생성 및 설정
    ```
	@Configuration
	@EnableSwagger2
	@Import(BeanValidatorPluginsConfiguration.class)
	public class FiSwaggerConfig {
	    private static final String API_NAME = "";

	    @Bean
	    public Docket fiApi() {

		TypeResolver typeResolver = new TypeResolver();
		return new Docket(DocumentationType.OAS_30)
			.ignoredParameterTypes(AuthenticationPrincipal.class)
			.tags(
				new Tag("", ""),
			)
			.groupName("")
			.select()
			.apis(RequestHandlerSelectors.basePackage(""))
			.paths(PathSelectors.any())
			.build()
			.apiInfo(this.apiInfo());
    }

    private ApiInfo apiInfo() {
        return new ApiInfoBuilder()
                .title(API_NAME)
                .build();
    }
    ```
* 참고: https://velog.io/@jeong-god/Spring-boot-Swagger-API-%EC%97%B0%EB%8F%99%ED%95%98%EA%B8%B0
* 참고: https://lucas-owner.tistory.com/28


## lombok
1. 의존성 추가
  - build.gradle에서 dependency 추가
    ```
    # lombok plugin
    implementation('org.projectlombok:lombok')
    annotationProcessor('org.projectlombok:lombok')    

    # test 환경
    testImplementation('org.projectlombok:lombok')
    testAnnotationProcessor('org.projectlombok:lombok')
    ```
* 참고: https://inpa.tistory.com/entry/IntelliJ-%F0%9F%92%BD-Lombok-%EC%84%A4%EC%B9%98-%EB%B0%A9%EB%B2%95-%EC%98%A4%EB%A5%98-%ED%95%B4%EA%B2%B0


## QueryDsl
1. version 정보 추가
	```
	buildscript {
	    ext {
		queryDslVersion = "5.0.0"
	    }
	}

	plugins {
	id "com.ewerk.gradle.plugins.querydsl" version "1.0.10"
	    id 'java'
	}
	```
2. 의존성 추가
	```
	implementation "com.querydsl:querydsl-jpa:${queryDslVersion}"
	implementation "com.querydsl:querydsl-apt:${queryDslVersion}"
	```
3. 설정 추가
	```
	// querydsl에서 사용할 경로 설정
	def querydslDir = "$buildDir/generated/querydsl"
	// JPA 사용 여부와 사용할 경로를 설정
	querydsl {
	    jpa = true
	    querydslSourcesDir = querydslDir
	}
	// build 시 사용할 sourceSet 추가
	sourceSets {
	    main.java.srcDir querydslDir
	}
	// querydsl 컴파일시 사용할 옵션 설정
	compileQuerydsl{
	    options.annotationProcessorPath = configurations.querydsl
	}
	// querydsl 이 compileClassPath 를 상속하도록 설정
	configurations {
	    compileOnly {
		extendsFrom annotationProcessor
	    }
	    querydsl.extendsFrom compileClasspath
	}
	```
* 참고: https://data-make.tistory.com/728
