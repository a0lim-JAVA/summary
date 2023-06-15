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
    implementation 'io.springfox:springfox-boot-starter:3.0.0'
	  implementation 'io.springfox:springfox-swagger-ui:3.0.0'
	  implementation 'io.springfox:springfox-bean-validators:3.0.0'
    ```
  - swaggerConfig 파일 생성 및 설정
    ```
* 참고: https://inpa.tistory.com/entry/IntelliJ-%F0%9F%92%BD-Lombok-%EC%84%A4%EC%B9%98-%EB%B0%A9%EB%B2%95-%EC%98%A4%EB%A5%98-%ED%95%B4%EA%B2%B0
