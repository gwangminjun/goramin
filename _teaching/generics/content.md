---
title: "Generics"
collection: teaching
type: "java"
permalink: /teaching/generics/content
venue: "회사"
date: 2024-09-10
---
Generics 에 대해서

## 서론
   현재 회사코드에서는 DTO 구조로 구성되어있어 제네릭은 사용하지 않는데 <br>
   typeScript 스터디를 진행하면서 타입추론에 관심을 가지게 되고 <br>
   제네릭에 대해서 관심이 생겨 정리하게 되었다

### java 제네릭
   자바의 제네릭(Generics)은 Java 5부터 도입된 기능으로, <br>
   클래스나 메서드에서 사용할 타입을 파라미터로 받아서 유연하고 재사용성 높은 코드를 작성할 수 있도록 해줍니다. <br> 
   제네릭을 사용하면 컴파일 시점에 타입을 체크하므로 런타임 에러를 방지할 수 있습니다. <br>

#### 제네릭 클래스 정의 , 사용
   ```java
   public class Box<T> {
       private T item;
   
       public void setItem(T item) {
           this.item = item;
       }
   
       public T getItem() {
           return item;
       }
   }
   
   // Box<String> stringBox = new Box<>();
   // stringBox.setItem("Hello, Generics!");
   // String item = stringBox.getItem();
   //
   // Box<Integer> integerBox = new Box<>();
   // integerBox.setItem(42);
   // int number = integerBox.getItem();
   ```
#### 제네릭 메서드 정의 , 사용
   ```java
   public static <T> void printArray(T[] array) {
       for (T element : array) {
           System.out.print(element + " ");
       }
       System.out.println();
   }
   
   // Integer[] intArray = {1, 2, 3, 4, 5};
   // Double[] doubleArray = {1.1, 2.2, 3.3, 4.4, 5.5};
   // String[] stringArray = {"A", "B", "C", "D", "E"};
   //
   // printArray(intArray);    // 1 2 3 4 5
   // printArray(doubleArray); // 1.1 2.2 3.3 4.4 5.5
   // printArray(stringArray); // A B C D E
   ```

### 제네릭 활용법
1. 타입 매개변수 제한하기
   - extends 키워드를 사용하여 매개변수를 클래스나 인터페이스로 제한
   - 
```java
public class Box<T extends Number> {
   private T value;

   public void setValue(T value) {
       this.value = value;
   }

   public T getValue() {
       return value;
   }
}

//정상
// Box<Integer> intBox = new Box<>();
// intBox.setValue(10);
// Integer value = intBox.getValue();
//
// Box<Double> doubleBox = new Box<>();
// doubleBox.setValue(3.14);
// Double value = doubleBox.getValue();

//컴파일 에러
//Box<Integer>, Box<Double> 등으로 사용할 수 있지만, Box<String>은 컴파일 에러가 발생합니다. 
//왜냐하면 String은 Number의 하위 클래스가 아니기 때문입니다.
// Box<String> stringBox = new Box<>();
```
2. 와일드 카드 표현
   - 제네릭 타입에서 ?를 사용하여 와일드카드를 표현할 수 있습니다.
   - "<? extends T>": T의 하위 클래스만 허용 (상한 경계)
   - "<? super T>": T의 상위 클래스만 허용 (하한 경계)
   - "<?>": 모든 타입 허용
   ```java
   public static void printList(List<? extends Number> list) {
      for (Number item : list) {  \
          System.out.println(item);
          }
   }
   // List<Integer>, List<Double> 등의 리스트를 전달할 수 있지만, 
   // List<String>은 컴파일 에러가 발생
   ```
3. 제네릭 인터페이스
   - 제네릭으로 정의된 인터페이스
   ```java
   public interface Pair<K, V> {
     K getKey();
     V getValue();
   }
   // pair 인터페이스를 구현하는 OrderPari 클래스
   // public class OrderedPair<K, V> implements Pair<K, V> {
   //  private K key;
   //  private V value;
   //
   //  public OrderedPair(K key, V value) {
   //      this.key = key;
   //      this.value = value;
   //  }
   //
   //  public K getKey() {
   //      return key;
   //  }
   //
   //  public V getValue() {
   //      return value;
   //  }
   // }   
   ```
   
   
   
   
4. 다중 타입 매개변수
   - 클래스나 메서드에서 여러 개의 타입 매개변수를 사용
   ```java
   public class Pair<K, V> {
       private K key;
       private V value;
   
       public Pair(K key, V value) {
           this.key = key;
           this.value = value;
       }
   
       public K getKey() {
           return key;
       }
   
       public V getValue() {
           return value;
       }
   }
   ```
5. 제네릭 메서드와 타입 추론
   - 메서드 선언부에 타입 매개변수를 사용하여 제네릭 메서드를 정의
   - Java 7부터는 타입 추론을 지원하여, 메서드 호출 시 타입 매개변수를 명시하지 않아도 된다.
   ```java
   public static <T> List<T> createList(T... elements) {
       return Arrays.asList(elements);
   }
   //메서드 호출 시 타입 인자를 명시하지 않아도 컴파일러가 전달된 인자를 기반으로 타입을 추론
   //createList("A", "B", "C")와 같이 호출하면 List<String>이 반환되고, 
   //createList(1, 2, 3)와 같이 호출하면 List<Integer>가 반환
   ```

6. 제네릭 타입 삭제
   - 자바의 제네릭은 컴파일 시점에만 타입 체크를 수행하고, 런타임에는 제네릭 타입 정보가 삭제된다.
   - 이를 타입 삭제라고 하며, 이로 인해 제네릭 타입의 인스턴스를 만들거나 instanceof 연산자를 사용할 수 없습니다.
   
7. 제네릭 타입의 상속
   - 제네릭 클래스나 인터페이스를 상속할 때, 타입 매개변수를 지정해야 합니다.
```java
public class Box<T> {
    protected T value;

    public void setValue(T value) {
        this.value = value;
    }

    public T getValue() {
        return value;
    }
}
// box 클래스를 상속받는 IntegerBox 클래스
// public class IntegerBox extends Box<Integer> {
//     public void increment() {
//         value++;
//     }
// }
```

### 일반적인 타입 매개변수 선언
1. T (Type): 일반적인 타입을 나타낼 때 주로 사용됩니다. 
   - List<T>에서 T는 리스트에 저장될 요소의 타입을 나타냅니다.
2. K (Key): 키-값 쌍(Key-Value pair)에서 키(Key)의 타입을 나타낼 때 주로 사용됩니다. 
   - Map<K, V>에서 K는 맵의 키 타입을 나타냅니다. 
3. V (Value): 키-값 쌍에서 값(Value)의 타입을 나타낼 때 주로 사용됩니다. 
   - Map<K, V>에서 V는 맵의 값 타입을 나타냅니다. 
4. E (Element): 컬렉션(Collection)에서 요소(Element)의 타입을 나타낼 때 주로 사용됩니다. 
   - List<E>에서 E는 리스트의 요소 타입을 나타냅니다. 
5. N (Number): 숫자(Number) 타입을 나타낼 때 주로 사용됩니다.

### 제네릭 vs DTO

|   비교    | 제네릭                                                       | DTO                                                         |
|:-------:|:----------------------------------------------------------|:------------------------------------------------------------|
|  타입검사   | 컴파일 시점                                                    | 런타임 시점                                                      |
|  타입캐스팅  | 타입 캐스팅 오류 방지                                              | 타입 캐스팅 오류 발생 가능                                             |
|  타입 사용  | 잘못된 타입 사용 방지                                              | 잘못된 타입 사용 가능                                                |
| 타입 매개변수 | - 타입 매개변수를 사용하여 코드 작성 <br> 실제 사용 시 구체적인 타입으로 대체           | - 클래스 정의 시 구체적인 타입 사용<br>- 타입 매개변수 사용하지 않음                  |
| 코드 재사용성 | - 높음 <br> - 다양한 타입에 대해 동일한 코드 재사용 가능<br> - 유지보수성 향상       | - 낮음 <br> - 특정 타입에 종속적인 코드 <br>- 코드 중복 발생 가능                |
|   용도    | - 컬렉션, 알고리즘, 자료구조 등에 사용<br>- 타입에 종속되지 않는 일반화된 코드 작성       | - 계층 간 데이터 전송에 사용<br>- 데이터 구조 정의 및 캡슐화                      |
| 데이터 전송  | - 데이터 전송을 주 목적으로 하지 않음<br>- 타입 안전성과 코드 재사용성에 초점           | - 계층 간 데이터 전송이 주 목적<br>- 데이터 구조의 일관성과 안정성 보장                |
|   성능    | - 제네릭 타입 삭제로 인한 런타임 오버헤드 없음<br>- 컴파일 타임에 타입 검사 수행으로 성능 향상 | - 객체 생성과 복사로 인한 성능 오버헤드 발생 가능<br>- 런타임에 타입 검사 수행으로 성능 저하 가능 |

#### 성능 오버헤드 관련

|   비교    | 제네릭                                                               | DTO                                                                                         |
|:-------:|:------------------------------------------------------------------|:--------------------------------------------------------------------------------------------|
|  객체생성   | - 타입 매개변수를 사용하여 객체 생성 시점에 타입을 지정합니다. <br> - 추가적인 오버헤드가 발생하지 않습니다. | - 계층 간 데이터 전송을 위해 새로운 객체를 생성해야 합니다. <br>- 빈번한 객체 생성은 성능 오버헤드를 유발할 수 있습니다. <br>              |
|  객체복사   | - 객체 복사와는 관련이 없습니다.                                               | -  사용할 때 도메인 객체나 엔티티의 데이터를 DTO로 복사하는 작업과 그 반대의 작업이 필요 <br> 이러한 복사 작업은 성능 오버헤드를 유발할 수 있습니다.  |
| 네트워크 전송 | - 네트워크 전송과는 무관.                                                   | -  직렬화와 역직렬화 과정에서 오버헤드가 발생할 수 있습니다. <br> - 전송할 데이터의 크기가 클수록 오버헤드가 증가                        |
|   런타임   | - 컴파일 타임에 타입 검사를 수행하고 런타임에는 타입 정보가 제거되므로, 런타임 오버헤드가 발생하지 않습니다.    | - 런타임에 객체로 존재하므로 메모리 사용량이 증가할 수 있습니다. <br> - DTO 객체의 생성과 가비지 컬렉션으로 인한 런타임 오버헤드가 발생할 수 있습니다. |

### object vs T
   - object 로 선언시와 타입 선언시 의 차이
   -
   ```java
   public class objectDataDTO {
       private Object data;
   }
   
   public class genericDataDTO {
      private T data;
   }
   ```

|  비교   | 제네릭                                  | Object                                                           |
|:-----:|:-------------------------------------|:-----------------------------------------------------------------|
| 타입검사  | 컴파일 시점                               | 런타임시점                                                            |
| 타입안정성 | 보장                                   | 미보장                                                              |
| 타입캐스팅 | - 불필요 <br> - 타입 매개변수 사용              | - 필요 <br> - 사용시 적절한 타입으로 캐스팅                                     |
|  유연성  | - 자바의 최상위 클래스 <br> - 모든 타입의 객체 저장 가능 | - 타입 매개변수의 제약 <br> - 참조 타입만 사용 가능 <br> - 원시타입 직접사용 불가 , 래퍼클래스 사용 |
