# TIL 200604(Thu)

# 알고리즘



## Queue(큐) - 자바에서 제공하는 큐 사용하기.



### 큐란

큐는 스택과 만찬가지로 데이터를 일시적으로 쌓아 두기 위한 자료구조이다. 

스택과의 차이점은 선입선출(First-In-First-Out) 구조라는 것이다. 

큐의 예로 마트에서 계산을 기다리는 대기열을 떠올릴 수 있다. 

 

큐에 데이터를 넣는 작업을 인큐(Enqueue)라고 하고, 데이터를 꺼내는 작업을 디큐(Dequeue)라고 한다.

또 데이터를 꺼내는 쪽을 프론트(Front), 넣는 쪽을 리어(Rear)라고 한다. 

 

### 큐 사용해보기. 

자바에서 제공하는 큐를 사용해보자. 

 

Java에서 제공하는 Queue의 경우 인터페이스이기 때문에 객체 생성이 불가능하다. 
따라서 LinkedList를 이용한다. 

 

(LinkedList를 이용한) 큐는 다음과 같은 메소드를 가진다. 

 

**add**

add는 queue의 맨 앞에 요소를 집어넣는다. 

 

**peek**

peek은 queue의 맨 앞에 있는 요소를 리턴한다. 

 

**poll** 

poll은 queue의 맨 앞에 있는 요소를 삭제하고 리턴한다. 



**toString** 

toString을 통해 queue에 어떤 요소들이 남아있는지 확인한다.  

 

**contains**  

contains를 통해 queue에 특정 요소가 있는지 확인한다. 

 

**size**

size를 통해 queue에 요소가 몇 개 있는지 확인한다.



**clear**

clear를 통해 queue의 요소를 모두 삭제한다.

 

### 코드로 확인하기

 

```java
import java.util.LinkedList;
import java.util.Queue;

public class QueueMethods {
	
	public static void main(String[] args) {
		Queue<Integer> intQueue = new LinkedList<>();
		
		System.out.println(intQueue.isEmpty());
		//true
		intQueue.add(1);
		intQueue.add(2);
		intQueue.add(3);
		
		System.out.println(intQueue.peek()); //1
		System.out.println(intQueue.contains(1));  //true
		System.out.println(intQueue.poll()); //1
		System.out.println(intQueue.contains(1)); //false
		
		String intQueueString = intQueue.toString();
		System.out.println(intQueueString);
		
		System.out.println(intQueue.size());
		//2출력, {2, 3}
		intQueue.clear();
		System.out.println(intQueue.isEmpty()); //true
    }
}

```





### 큐 직접 만들어보기

 

```java
//GQueue<E> 클래스

public class GQueue<E>{
	private int front;
	private int rear;
	private int count;
	private int max;
	private E [] queue;
	
	public GQueue(int capacity) {
		this.front = 0;
		this.rear = 0;
		this.max = capacity;
		this.count = 0;
		this.queue = (E[]) new Object[capacity];
	}

	public E enqueue(E param) throws RuntimeException {
		if (count >= max)
			throw new RuntimeException();
		queue[rear++] = param;
		count++;
		return param;
	}
    
	public E peek() throws RuntimeException {
		if (count == 0)
			throw new RuntimeException();
		return queue[front];
	}
	
	public E poll() throws RuntimeException {
		if (count == 0)
			throw new RuntimeException();
		System.out.println(queue[front]);
		for (int i = 1; i <= count; i++) {
			queue[i - 1] = queue[i];
		}
		count--;
		rear--;
		return queue[front++];
	}
	
	public void clear() {
		count = front = rear = 0;
	}
	
	public int size() {
		return count;
	}
	
	public boolean isEmpty() {
		return count == 0;
	}
	
	public String dump() {
		String result = "";
		
		for (int i = 0; i < count; i++) {
			result += i + "번쨰  요소 : " + (String)queue[i] + "\n";
		}
		return result;
	}
}
```

* 참고 - 제네릭 타입 배열 필드를 가지고 있는 제네릭 클래스를 만드는 법에 관한 글

  : (링크)[https://brunch.co.kr/@oemilk/143]

```java
//main 클래스

public class GenericQueue {
	public static void main(String[] args) {
		GQueue<String> queue = new GQueue<>(10);
		
		queue.enqueue("hello");
		queue.enqueue("world");
		queue.enqueue("I'm Java!");
		
		System.out.println(queue.peek()); //hello출력
		System.out.println(queue.size()); //3 출력
		System.out.println(queue.poll()); //world 출력
		
		System.out.println(queue.dump());
		//0번쨰  요소 : world
		//1번쨰  요소 : I'm Java!
		queue.clear();
		System.out.println(queue.isEmpty());
        //true
		
	}
	
}
```

 

* enqueue할 때 count == max가 된 경우 rear를 0으로 설정해주면 링 버퍼(원형)가 된다.







