## Java Thread

목차

1. [Socket](#socket)

* * *

### Socket

#### 1. Socket Server

```java
public class TestSocketServer {

  public static void main(String[] args) throws IOException {

    ServerSocket serverSocket = new ServerSocket(8080);
    BufferedReader br;
    PrintWriter pw;

    while(true){
      Socket socket = serverSocket.accept();

      try{
        InputStream in =socket.getInputStream();
        OutputStream out = socket.getOutputStream();

        br = new BufferedReader(new InputStreamReader(in));
        pw = new PrintWriter(new OutputStreamWriter(out));

        String line = null;
        while ((line = br.readLine()) != null) {
          if(line.equals("q")){
            break;
          }
          System.out.println(line);
        }
        pw.println("읽기 완료!!");
        pw.flush();

      } catch(Exception e){
        e.printStackTrace();
      } finally{
        try {
          socket.close();
        } catch (IOException e) {
          e.printStackTrace();
        }
      }
    }
  }
}
```
#### 2. Socket Client

```java
public class TestSocketClient {

  public static void main(String[] args) {

    Socket socket = null;
    BufferedReader br;
    PrintWriter pw;

    try {
      socket = new Socket("127.0.0.1", 8080);
      InputStream in =socket.getInputStream();
      OutputStream out = socket.getOutputStream();

      br = new BufferedReader(new InputStreamReader(in));
      pw = new PrintWriter(new OutputStreamWriter(out));

      pw.println("여보세요");
      pw.println("안녕하세요");
      pw.println("q");
      pw.flush();

      System.out.println(br.readLine());

    } catch (Exception e) {
      e.printStackTrace();
    } finally {
      try {
        socket.close();
      } catch (IOException e) {
        e.printStackTrace();
      }
    }
  }
}
```

#### 3. Socket Server + Thread Pool

```Java
public class TestSocketServerWithThreadPool {

  public static void main(String[] args) throws IOException {

    ServerSocket serverSocket = new ServerSocket(8080);
    ExecutorService executor = Executors.newFixedThreadPool(10);

    while(true){
      Socket socket = serverSocket.accept();
      try{
        executor.execute(new SocketConnection(socket));
      } catch(Exception e){
        e.printStackTrace();
      }
    }
  }
}

class SocketConnection implements Runnable{

  private Socket socket = null;

  public SocketConnection(Socket socket) {
    this.socket = socket;
  }

  @Override
  public void run() {

    BufferedReader br;
    PrintWriter pw;

    try{
      InputStream in =socket.getInputStream();
      OutputStream out = socket.getOutputStream();

      br = new BufferedReader(new InputStreamReader(in));
      pw = new PrintWriter(new OutputStreamWriter(out));

      String line = null;
      while ((line = br.readLine()) != null) {
        if(line.equals("q")){
          break;
        }
        System.out.println(line);
      }
      pw.println("읽기 완료!!");
      pw.flush();

    } catch(Exception e) {
      e.printStackTrace();
    } finally {
      try {
        socket.close();
      } catch (IOException e) {
        e.printStackTrace();
      }
    }
  }
}
```

* * *

### [References]
1. N/A
