### Java

1. 쓰레드에서 main메소드 종료 전에 모두 일을 끝마치도록 설정하기(Join 메소드)<br>

   - 쓰레드를 이용하면 내가 실행한 메소드들이 순서대로 실행되지 않을 뿐더러, main메소드가 종료되기 전에 끝나지 않아 main메소드 이후에도 돌아간다.

   - 이런 상황에서 main메소드가 끝나기 전에 모든 쓰레드를 실행, 종료시키는 방법이 있다.<br><br>

   - ```java
     public class ThreadTestJoin extends Thread {
     
     	private int seq;
     
     	public ThreadTestJoin(int seq) {
     		this.seq = seq;
     	}
     
     	@Override
     	public void run() {
     		System.out.println(this.seq + "thread start");
     		try {
     			Thread.sleep(1000);
     		} catch (Exception e) {
     			e.printStackTrace();
     		}
     		System.out.println(this.seq + "thread end");
     	}
     
     	public static void main(String[] args) {
     		List<Thread> threadList = new ArrayList<>();
     		for (int i = 0; i < 10; i++) {
     			Thread t = new ThreadTestJoin(i);
     			t.start();
     			threadList.add(t);
     		}
     		
     		for (int i = 0; i < threadList.size(); i++) {
     			Thread t = threadList.get(i);
     			try {
     				t.join();
     			} catch (Exception e) {
     				e.printStackTrace();
     			}
     		}
     		System.out.println("main end");
     	}
     
     }
     
     ```

     <br><br>위의 코드를 크게 두 부분으로 살펴보면 <br><br>

     1. ThreadTestJoin(i)를 통해 Thread를 생성하여 start 메서드를 적용하는 부분.
     2. threadList에 t를 담아 join시키는 부분이 있다.<br><br>

     즉, thread 하나 하나를 하나의 arrayList에 담고 모두 join() 시켜버리면 main메소드가 끝나기 전에 모든 쓰레드가 처리된다. 결과는 아래와 같다.<br><br>

     ```java
     0thread start
     3thread start
     4thread start
     2thread start
     1thread start
     5thread start
     6thread start
     7thread start
     8thread start
     9thread start
     5thread end
     3thread end
     4thread end
     1thread end
     2thread end
     0thread end
     8thread end
     7thread end
     9thread end
     6thread end
     main end
     ```

     <br><br>

2. Runnable 인터페이스를 구현하여 Thread 이용하기<br><br>

   - Thread를 이용하기 위해 Thread 클래스를 상속하는 방법도 있지만, Runnable 인터페이스를 구현하는 방법도 있다. 예제를 통해 살펴보자. 참고로 Runnable 인터페이스를 구현하면 반드시 run 메소드를 오버라이드 해야 한다.<br><br>

     ```java
     public class ThreadRunnable implements Runnable {
     
     	private int seq;
     	
     	public ThreadRunnable(int seq) {
     		this.seq = seq;
     	}
     	
     	@Override
     	public void run() {
     		System.out.println(this.seq + "thread start");
     		try {
     			Thread.sleep(1000);
     		} catch (Exception e) {
     			e.printStackTrace();
     		}
     		System.out.println(this.seq + "thread end");
     	}
     	
     	public static void main(String[] args) {
     		List<Thread> threadList = new ArrayList<>();
     		for (int i = 0; i < 10; i++) {
     			Thread t = new Thread(new ThreadRunnable(i));
     			t.start();
     			threadList.add(t);
     		}
     		
     		for (int i = 0; i < threadList.size(); i++) {
     			Thread t = threadList.get(i);
     			try {
     				t.join();
     			} catch (Exception e) {
     				e.printStackTrace();
     			}
     		}
     		System.out.println("main end");
     	}
     	
     }
     ```

     <br><br>위 join메소드 예제와 달라진 부분은 단 두 곳이다. 먼저 맨 윗줄에<br><br>

     ```java
     public class ThreadRunnable implements Runnable {
     ```

     <br><br>여기서 extends 하던 것을 implements 하고 있다는 것, 그리고<br><br><br>

     ```java
     Thread t = new Thread(new ThreadRunnable(i));
     ```

     <br>Thread를 생성할 때 Runnable인터페이스를 구현한 클래스의 인스턴스를 Thread의 생성자로 넘겨준다는 것. 특히 이 부분에서 Runnable 인터페이스를 구현한 클래스의 인스턴스를 Thread의 생성자로 넘겨주면 우리가 설정한 run 메소드를 가지고 있는 쓰레드가 생성된다는 것을 알 수 있다.