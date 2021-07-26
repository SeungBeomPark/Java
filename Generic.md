**Generics**



■ **Generics**

제네릭(Generics)란 무엇인가? 간단하게 컬렉션 ArrayList와 List를 통해 알아보겠다.

ArrayList와 List 등 컬렉션을 사용할 때 아래와 같이 선언을 해준다.

// ArrayList

ArrayList<String> arrList = new ArrayList<String>();

// List

List<Integer> list = new ArrayList<Integer>();



현재 ArrayList를 보면 <>안에 String, List에는 <>안에 int형을 나타내는 Integer가 들어가 있다.



이 <>를 제네릭(Generics)이라 하는데, 이 <>안에 어떠한 타입을 선언해주어 해당 ArrayList, List 등이 사용할 객체의 타입을 지정해준다는 뜻이다. 이는 다룰 객체의 타입을 미리 명시하여 객체의 형변환을 사용할 필요없게 하며, 내가 사용하고 싶은 데이터 타입만 사용할 수 있게 해주는 효과가 있습니다. 

```java
import java.util.ArrayList;
import java.util.List;
 
public class Generics {
 
    public static void main(String[] args) {
        
        ArrayList<String> arrList = new ArrayList<String>();
        
        arrList.add("박지성");
        arrList.add("손흥민");
        arrList.add("기성용");
        
        for(int i=0; i<arrList.size(); i++){
            System.out.println("arrList : " + arrList.get(i));
        }
        
        List<Integer> list = new ArrayList<Integer>();
        list.add(123);
        list.add(456);
        list.add(789);
        
        for(int i=0; i<list.size(); i++){
            System.out.println("list : " + list.get(i));
        }
    }
 
}
```



위의 예시를 보면,



ArrayList는 String으로 선언해주어, ArrayList는 String 객체만 다루게 되며,

List는 Integer로 선언해주어, List는 int형 객체만 다루게 됩니다.



![img](https://t1.daumcdn.net/cfile/tistory/997F71435AD553700A)



이렇듯 미리 사용할 객체의 타입을 명시해 주었기에 다음과 같이 제네릭과 맞지않는 객체의 타입이 올 경우 컴파일 에러가 발생하게 됩니다.



위의 예시를 통해 제네릭(Generics)은 크게 2가지의 장점을 가지고 있다.



\1. 타입의 안정성 : 의도하지 않은 타입의 객체가 저장되는 것을 막고, 다른 타입의 객체로 인한 타입 형태가 맞지 않아 발생하는 문제를 없애준다.

\2. 불필요한 형변환을 줄여 코드의 간결함 : 타입을 미리 명시함으로써 다른 타입의 객체가 저장되지 않아 객체를 꺼내 사용할 시 형변환을 통한 타입을 맞출 필요가 없어 코드를 간결하게 줄일 수 있다.





■ **Generics의 다형성**

제네릭(Generics)에도 다형성 개념을 사용할 수 있다. 

위에서 제네릭(Generics)에 대해 알아볼때는 ArrayList라던지 List 등 컬렉션의 사용에서 예시를 들었는데 제네릭(Generics)은 컬렉션에서만 사용되는 개념이 아니고 클래스, 인터페이스 등 다양하게 사용될 수 있다. 

이번 다형성의 예시는 클래스 타입 제네릭(Class Generic type)으로 예시를 들어보겠다.

```java
public class Generics {
 
    public static void main(String[] args) {
        
        ArrayList<Sports> arrList = new ArrayList<Sports>();
        arrList.add(new Sports());
        arrList.add(new Soccer());
        arrList.add(new Baseball());
        
        Sports sports = arrList.get(0);
        Soccer soccer = (Soccer) arrList.get(1);
    }
 
}
 
class Sports{}
 
class Soccer extends Sports{}
 
class Baseball extends Sports{}
```

위의 예시를 보면, Sports라는 클래스 타입의 ArrayList를 생성하였다.

Sports클래스는 부모 클래스로 하위(자식)클래스인 Soccer, Baseball 클래스가 부모클래스를 상속받고 있다.

**6~8번째 라인)**을 보면 부모 클래스 본인 뿐만아니라 Soccer와 Baseball 객체도 부모클래스 타입으로 선언된 ArrayList에 저장될 수 있다.

이는 바로 제네릭(Generics)의 다형성으로 부모클래스로부터 상속을 받았기에 가능한것이다.

![img](https://t1.daumcdn.net/cfile/tistory/996D554C5AD5797037)



다만, **15~16번째 라인)**에서 처럼 해당 ArrayList에서 객체를 꺼낼때 부모 본인은 문제가 없지만 자식클래스는 본인의 타입으로 다시 형변환을 해주어야 한다.



부모와 자식간의 상속관계가 있다하여도 다음과 같이 사용할 수는 없다.



ArrayList<Sports> arrList = new ArrayList<Soccer>();



■ **와일드카드**



제네릭(Generics)은 보통 하나의 타입을 지정, 명시하지만 하나 이상의 타입을 지정해야 하는 경우가 발생할 수 있다. 이를 위해 와일드카드라는 것을 이용해 해결할 수 있다.



와일드카드란 '?'를 이용해 하나 이상의 타입을 가능하게 하는데 여기서 ?는 어떤 타입도 가능하다는 랜덤의 뜻이 아닌가 싶다(?)



1. ArrayList<**? extends Sports**> arrList = new ArrayList<>();

2. ArrayList<**?**> arrList = new ArrayList<>();

3. ArrayList<**? super Soccer**> arrList = new ArrayList<>();



이렇게 3가지 형태로 와일드카드를 쓸 수 있는데,

예를 들어 Sports라는 운동종목을 통틀으는 최상위 클래스가 있다고 하자.

간단히 Sports 하위 클래스로 Skating과 Golf라는 클래스가 존재하며, Skating 클래스 하위에는 SortTrack과 SpeedSkating이라는 하위 클래스가 존재한다. 

다음과 같은 그림이 될텐데,



![img](https://t1.daumcdn.net/cfile/tistory/99EF1C3E5AD583A822)



여기서 와일드카드의 쓰임에 따라 추가가 허용되는 타입의 범위가 달라진다.



**1. ArrayList<?> arrList :** 와일드카드 ?만 왔음으로 모든 스포츠 Sports클래스의 하위 클래스 타입이 올 수 있다.

**2. ArrayList<? extends Skating> arrList** **:** Skating과 이를 상속받은 SpeedSkating, SortTrack이 타입으로 올 수 있다.

**3. ArrayList<? super Golf> arrList** **:** Golf와 함께 Sports클래스 타입만 올 수 있다.



■ **복수(여러개)의 Generics 사용법**

클래스 내에서 여러개의 제네릭(Generics)을 필요로 하는 경우가 있다.

복수의 제네릭(Generics)을 사용해야 할 경우 **8번째 라인)**과 같이 ','를 이용해 복수의 제네릭(Generics)을 명시해주면 된다.