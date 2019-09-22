---
layout: post
title:  "[스터디 기록][2장] spring 5 recipes 2-6~2-10"
date:   2018-07-10 10:00
author: jizero
tags:	['springFramework',' spring recipes 5']
---



### 외부 리소스 데이터 사용하기

[1.properties](http://1.properties) 읽기

@PropertySource("classpath:discounts.properties")

@Value("${specialcustomer.discount:0}")

2..txt파일 가져오기

@PostConstruct로 인해 IoC 컨테이너 구성시점에 배너가 출력됨

    @PostConstruct
        public void showBanner() throws IOException {
            Files.lines(Paths.get(banner.getURI()), Charset.forName("UTF-8"))
                 .forEachOrdered(System.out::println);
        }

3.xml

    ClassPathXmlApplicationContext context = 
    new ClassPathXmlApplicationContext("classpath:beans.xml");

### 다국어 메시지해석

messages_en_US.properties
MyResource_en.properties
MyResource.properties
즉, 자동으로 JVM의 Locale 정보를 찾아서 위 순서대로 프로퍼티 파일을 순차적으로 찾는다.
Locale 옵션을 주지 않으면, Locale.getDefault()를 한다.

### 애네테이션을 이용해 POJO 초기화/폐기 커스터마이징

1.@Bean(initMethod = "openFile", destroyMethod = "closeFile")

2.@PreDestroy @Postconstruct   초기화/폐기 메서드 지정하기

3.@Lazy  느긋하게 초기화하기

4.@dependsOn 초기화순서정하기

### POJO 검증/수정

모든 빈 인스턴스를 처리하는  후처리기

BeanPostProcessor 이용하기

[https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/config/BeanPostProcessor.html](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/config/BeanPostProcessor.html)

 주어진 빈 인스턴스만

instanceof 연산자 이용하기  

부모 클래스 참조 변수 **instanceof** 연산(타입)

 instanceof는 객체타입을 확인하는데 사용한다. 속성은 연산자이고 형변환이 가능한 지 해당 여부를 true 또는 false로 가르쳐준다.

 @required 로 프로퍼티 검사하기

값의 존재여부를 조사하고 BeanInitializationException 으로 예외전달

### 팩토리로 POJO 생성

팩토리 메서드

활용 : 은닉 / 생성할 객체 타입을 예측할 수 없을때

 1.정적 팩토리

  ProductCreator.java

    public static Product createProduct(String productId) {
            if ("aaa".equals(productId)) {
                return new Battery("AAA", 2.5);
            } else if ("cdrw".equals(productId)) {
                return new Disc("CD-RW", 1.5);
            } else if ("dvdrw".equals(productId)) {
                return new Disc("DVD-RW", 3.0);
            }
            throw new IllegalArgumentException("Unknown product");
        }

 2.인스턴스팩토리

  ProductCreator.java

    public Product createProduct(String productId) {
            Product product = products.get(productId);
            if (product != null) {
                return product;
            }
            throw new IllegalArgumentException("Unknown product");
        }

 3.스프링 팩토리 빈을 이용해 할인가가 적용된 인스턴스를 생성  (2_10_iii)

팩토리 빈

([https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/FactoryBean.html](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/FactoryBean.html))

* getObject() : 실제 객체 반환

* getObjectType() : 반환하는 객체의 타입 반환

* isSingleton() : 반환하는 객체가 싱글톤인지 여부

DiscountFactoryBean.java
```java
    @Override
        protected Product createInstance() throws Exception {
            product.setPrice(product.getPrice() * (1 - discount));
            return product;
        }
```



## 참고 사이트
[https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/config/AbstractFactoryBean.html](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/config/AbstractFactoryBean.html)


## 
매주 일요일 spring 5 recipes  정리본 
notion에 정리 중인 파일을 블로그에 옮긴글입니다.