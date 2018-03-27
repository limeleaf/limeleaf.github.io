## File 입출력

목차

1. [사용자 입력 처리](#사용자-입력-처리)
1. [File 입출력](#file-입출력)

* * *

### 사용자 입력 처리

#### 1. 사용자 입력 받아 읽어 보기

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
}
```
#### 2. Scanner 클래스 사용하기

```java
public class TestScanner {
  public static void main(String[] args) {
    Scanner sc = new Scanner(System.in);
    while(sc.hasNext()){
      String str = sc.next();
      System.out.println("입력 값 :"+str);
    }
  }
}
```

* * *

### File 입출력

#### 1. File을 읽어 다른 파일에 쓰기

```Java
public class TestFileReadWrite {

  public static void main(String[] args) throws IOException {

    BufferedReader br = new BufferedReader(new FileReader("./resources/test-in.txt"));
    //PrintWriter pw = new PrintWriter(new FileWriter("./resources/test-out.txt", true)); //append 하기
    PrintWriter pw = new PrintWriter(new FileWriter("./resources/test-out.txt", false));		

    String line = null;
    while((line = br.readLine()) != null) {
      System.out.println(line);
      pw.println("옮겨 적기 : " + line);
    }
    br.close();
    pw.close();
	}
}
```
#### 2. RandomAccessFile 이용하기

```Java
public class TestRandomAccess {

  public static void main(String[] args) throws IOException {

    RandomAccessFile rf = new RandomAccessFile("./resources/test-in.txt","rw");
    String line = "";

    System.out.println("(1) File의 길이 : " + rf.length());

    // A
    // BC
    // DEF
    System.out.println("(2) File의 내용 : ");
    while ((line = rf.readLine()) != null) {
      System.out.println("-> " + line);			
    }

    System.out.println("(3) 원하는 곳에 접근해 값 가져오기 : ");
    rf.seek(0);
    System.out.println("-> " + (char)rf.read()); // A

    rf.seek(1);
    System.out.println("-> " + rf.read());	// CR

    rf.seek(2);
    System.out.println("-> " + rf.read());  // LF

    rf.seek(3);
    System.out.println("-> " + (char)rf.read()); // B
    rf.write('Z');								// 덮어 쓰기

    // A
    // BZ
    // DEF
    System.out.println("(4) 수정된 File의 내용 : ");
    rf.seek(0);
    while ((line = rf.readLine()) != null) {
      System.out.println("-> " + line);			
    }

    rf.close();
  }
}
```

* * *

### [References]
1. N/A
