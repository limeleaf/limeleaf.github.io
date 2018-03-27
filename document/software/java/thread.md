## Java Thread

목차

1. [Arrays.sort](#arrays.sort)

* * *

### Thread

#### 1. Thread extends 하기

- 기본적인 사용법
```java
public class TestThread extends Thread {

  @Override
  public void run() {
    System.out.println(Thread.currentThread());
  }

  public static void main(String[] args) {
    for(int idx=0; idx<5; idx++) {
      Thread thread = new TestThread();
      thread.start();
    }
  }
}
```

- join() 메서드로 기다리기
```java
public class TestThreadWithJoin extends Thread {

  @Override
  public void run() {
    System.out.println("START : " + Thread.currentThread());
    try {
      Thread.sleep(3000);
    } catch (InterruptedException e) {
      e.printStackTrace();
    }
    System.out.println("END : " + Thread.currentThread());
  }

  public static void main(String[] args) {

    int size = 5;
    List<Thread> list = new ArrayList<Thread>();

    for(int idx=0; idx<size; idx++) {
      Thread thread = new TestThreadWithJoin();
      thread.start();
      list.add(thread);
    }

    for(int idx=0; idx<size; idx++) {
      try {
        list.get(idx).join();
      } catch (InterruptedException e) {
        e.printStackTrace();
      }
    }

    System.out.println("실행 끝");
  }
}
```

- synchronized 사용하기
```java
public class TestThreadWithJoinAndSync extends Thread {

  // 중략
  static int count = 0;
  static synchronized void increasCount() {
    count++;
  }

  @Override
  public void run() {
    System.out.println("START : " + Thread.currentThread());
    try {
      Thread.sleep(3000);
    } catch (InterruptedException e) {
      e.printStackTrace();
    }

    increasCount();

    System.out.println("END : " + Thread.currentThread());
  }
  // 중략
}
```

#### 2. Runnable implements 하기

- 기본적인 사용법
```Java
public class TestRunnable implements Runnable {

  @Override
  public void run() {
    System.out.println(Thread.currentThread());
  }

  public static void main(String[] args) {
    for(int idx=0; idx<5; idx++) {
      Runnable r = new TestRunnable();
      Thread thread = new Thread(r);
      thread.start();
    }
  }
}
```

* * *

### Executor

#### 1. Executor 사용법

- FixedThreadPool
- CachedThreadPool
- SingleThreadExecutor

```Java
public class TestExecutorWithFuture implements Runnable {

  @Override
  public void run() {
    try {
      Thread.sleep(3000);
    } catch (InterruptedException e) {
      e.printStackTrace();
		}
		System.out.println(Thread.currentThread());
	}

	public static void main(String[] args) throws InterruptedException {

    int size = 5;

    ExecutorService execService = Executors.newFixedThreadPool(2);
    // ExecutorService execService = Executors.newCachedThreadPool();
    // ExecutorService execService = Executors.newSingleThreadExecutor();

    List<Future> futureList = new ArrayList<Future>();
    for(int idx=0; idx<size; idx++) {
      futureList.add(execService.submit(new TestExecutorWithFuture()));
    }

    // 4초 기다려 보고,
    Thread.sleep(4000);

    // 아직 끝나지 않은 게 있다면, 종료하고
    for(int idx=0; idx<5; idx++) {
      if(!futureList.get(idx).isDone()){
        futureList.get(idx).cancel(true);
      }
    }

    // 1초 기다려 보고,
    Thread.sleep(1000);

    // 다 체크해 본다
    for(int idx=0; idx<5; idx++) {
      System.out.println(futureList.get(idx).isDone());
    }

    execService.shutdown();

    System.out.println("끝");
  }
}
```

#### 2. Callable-Future

```Java
public class TestCallableFuture implements Callable<String> {

  int count = 0;

  public TestCallableFuture(int count) {
    this.count = count;
  }

  @Override
  public String call() throws Exception {
    Thread.sleep(1000);
    return "SUCCESS : " + count;
  }

  public static void main(String[] args) {

    ThreadPoolExecutor executor = (ThreadPoolExecutor)Executors.newFixedThreadPool(2);
    List<Future<String>> resultList = new ArrayList<Future<String>>();

    for(int idx=0; idx<5; idx++) {
      Future<String> result = executor.submit(new TestCallableFuture(idx));
      resultList.add(result);
    }

    for(Future<String> future : resultList) {
      try {
        System.out.println("결과: " + " - " + future.get());
      } catch (Exception e) {
        e.printStackTrace();
      }
    }
    executor.shutdown();
  }
}
```


* * *

### [References]
1. N/A
