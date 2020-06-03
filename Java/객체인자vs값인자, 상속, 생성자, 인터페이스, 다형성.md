#### JAVA

1. Java 에서는 함수의 인자로 값을 전달하는 것과 객체를 전달하는 것이 서로 다르게 작동한다.

   <br>

   - 예제 : 

     ```java
     public static void main(String[] args) {
         Dog dog = new Dog();
         public void settingAgePrimitiveValue(int age){
             age++;
         }
         dog.settingAgePrimitiveValue(dog.age);
         dog.showAge();
         //1이 증가되지 않은 채로 나옴
         public void settingAgeByObject(Dog dog){
             dog.age++;
         }
         dog.showAge();
         //1이 증가돼서 나옴
     }
     ```
     
     <br>

2. 상속의 개념에 대해 배움.<br>

   * is - a 관계에 대해 배울 수 있었다.
     - Animal을 상속받는 Dog를 is - a 관계로 표현하면 Dog is a Animal 이다.<br>
   * 메소드 오버라이딩에 대해 알게됐다.<br>
     - Animal에서 setName이라는 메소드가 있었어도 그것을 상속받는 Dog에서 setName을 재정의할 수 있고, 이것을 오버라이딩 한다고 표현한다. 오버라이딩은 input, output이 같아야 한다.<br>
   * 메소드 오버로딩에 대해 알게됐다.<br>
     * 메소드 오버라이딩과는 달리 input이나 output이 다를 경우 오버로딩한다고 표현한다.<br>
     * 예를 들어 public void bark(int count)라는 메소드가 있다고 할 때,
       public void bark(String barkSound)와 같이 적어주면 인자로 int가 들어올 때와 String이 들어올 때 해당 메소드가 제각각 동작한다는 뜻이다.<br>
     * 자바는 다중상속을 지원하지 않는다는 것을 배웠다. 동일한 리턴값과 인자를 받는 동일한 이름의 메소드를 가진 두 가지 클래스를 상속할 경우 오류를 발생시키기 때문이다.<br>

3. 생성자의 개념에 대해 배움<br>

   * 클래스와 이름이 같으면서 리턴값이 없는 메소드를 생성자 메소드라고 한다.
   * 기본적으로 인자와 내용이 없는 형태로 알아서 선언되곤 한다.
   * 인자로 무언가를 받도록 설정하여 객체를 만들 때 반드시 채워야 하는 필드를 설정할 수 있다.
   * 생성자도 오버로딩을 통해 int를 받을 때와 String을 받을 때로 나눌 수 있다.<br>

4. 인터페이스에 대해 배움<br>

   * 인터페이스를 사용하는 이유와 사용방법을 배움.<br>

     - 사용하는 이유 + 사용법을 예로 들면

       ```java
       public class ZooKeeper{
           public void feed(Tiger tiger){
               System.out.println("feed meat to tiger");
           }
           public void feed(Lion lion){
               System.out.println("feed meat to lion");
           }
       }
       ```

       Zookeeper 클래스가 Tiger, Lion에 이어 Crocodile, Puma 등 객체가 추가될 때마다 메소드를 추가해야 하는 불편함을 없애기 위해서다.

       ```java
       public interface Predator {
           public void feed();
       }
       public class Tiger extends Animal implements Predator {
           private String name;
        
           public Tiger(String name){
               this.name = name;
           }
           public void feed(){
               System.out.println("feed meat" + this.name);
           }
       } 
       ```

       위와 같은 방식으로 Tiger, Lion, Crocodile 등의 클래스를 선언해주면 ZooKeeper 클래스는 이제 딱 한 줄만 쓰면 된다.

       ```java
       public class ZooKeeper {
           public void feed(Predator predator){
               predator.feed();
           }
       }
       ```

       <br>

     - 다형성(Polymorphism)의 개념<br>

       - 위에서의 예제에서 Tiger를 한번 살펴보자.
     
         ```java
         public class Tiger extends Animal implements Predator{
             
       }
         ```
     
       이 경우 Tiger tiger는 Tiger의 객체이자 Animal을 상속받는 객체이기도 하면서 Predator 인터페이스의 객체이기도 하다. 
         이처럼 하나의 객체가 여러 자료형을 가진다는 것을 두고 다형성이라고 한다.<br>

     - 추상클래스의 (대략적인) 개념<br>
     
       - 인터페이스의 경우 프로토타입만을 가지고 있다.
       - 추상클래스의 경우 프로토타입이 아닌 실제 메소드 구현 부분도 가질 수가 있다.
       - 추상클래스를 상속받는 클래스는 인터페이스를 상속받는 클래스처럼 반드시 추상클래스 내의 메소드를 써야 한다.<br>

