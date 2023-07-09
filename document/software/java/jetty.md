## Java Thread

목차

1. [Jetty Server](#Server)
2. [Jetty Clinet](#Client)

* * *

### Server

#### 1. Jetty Server

```java
import org.eclipse.jetty.server.Server;
import org.eclipse.jetty.server.ServerConnector;
import org.eclipse.jetty.servlet.ServletHandler;

public class JettyServer {
	
  public static void main(String[] args) throws Exception {
    new JettyServer().start();
  }

  private void start() throws Exception{
		
    // 1. Web Server, Server Connector 생성
    Server server = new Server();
    ServerConnector httpConector = new ServerConnector(server);
    httpConector.setHost("127.0.0.1");
    httpConector.setPort(8080);
    server.addConnector(httpConector);
		
    // 2. Servlet Handler 매핑
    ServletHandler servletHandler = new ServletHandler();
    servletHandler.addServletWithMapping(MyServlet.class, "/");
    server.setHandler(servletHandler);
		
    // 3. Web Server start
    server.start();
    server.join();
  }
}
```
#### 2. Custom Servlet

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Iterator;
import java.io.InputStream;

import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class MyServlet extends HttpServlet {

  private static final long serialVersionUID = 1L;
	
  protected void doGet(HttpServletRequest req, HttpServletResponse res) throws IOException {
				
    System.out.println("======================");
    System.out.println("Request URL : " + req.getRequestURL());
    System.out.println("Request URI : " + req.getRequestURI());
    System.out.println("Servlet Path : " + req.getServletPath());
    System.out.println("Context Path : " + req.getContextPath());
    System.out.println("PathTranslated : " + req.getPathTranslated());
    System.out.println("Query String : " + req.getQueryString());
    System.out.println("param1 : " + req.getParameter("key1"));
		
    Iterator<String> itr = req.getAttributeNames().asIterator();
    int num = 0;
    while(itr.hasNext()) {
      String attrName = itr.next();
      System.out.println("Attribute Name " + num + " : " + attrName);
    }
		System.out.println("======================");
		
    res.setStatus(200);
    res.getWriter().write("Welcome to my server.");
  }
	
  protected void doPost(HttpServletRequest req, HttpServletResponse res) throws IOException {
    
    System.out.println("======================");
    System.out.println("Request URI : " + req.getRequestURI());
    System.out.println("body : " + getBody(req));
		
    System.out.println("======================");
    	
    res.setStatus(200);
    res.getWriter().write("Welcome to my server.");
  }
    
  private static String getBody(HttpServletRequest request) throws IOException {
    	 
    String body = null;
    StringBuilder stringBuilder = new StringBuilder();
    BufferedReader bufferedReader = null;
 
    try {
      InputStream inputStream = request.getInputStream();
      if (inputStream != null) {
        bufferedReader = new BufferedReader(new InputStreamReader(inputStream));
        char[] charBuffer = new char[128];
        int bytesRead = -1;
        while ((bytesRead = bufferedReader.read(charBuffer)) > 0) {
          stringBuilder.append(charBuffer, 0, bytesRead);
        }
      }
    } catch (IOException ex) {
      throw ex;
    } finally {
      if (bufferedReader != null) {
        try {
          bufferedReader.close();
        } catch (IOException ex) {
          throw ex;
        }
      }
    }
 
    body = stringBuilder.toString();
    return body;
  }
}
```

### Client

#### 1. Jetty Client
```java
public class JettyClient {

  public static void main(String[] args) throws Exception {
		
    HttpClient httpClient = new HttpClient();
    httpClient.start();
		
    // Get 요청
    ContentResponse res = httpClient.newRequest("http://127.0.0.1:8080/biz/test1?key1=1&key2=2").method(HttpMethod.GET).send();
    System.out.println(res.getContentAsString());

    // Post 요청
    Request request = httpClient.newRequest("http://127.0.0.1:8080/fileList").method(HttpMethod.POST);
    request.header(HttpHeader.CONTENT_TYPE, "application/json");
    request.content(new StringContentProvider(getFileList(), "utf-8"));

    ContentResponse contentRes = request.send();
    System.out.println(contentRes.getContentAsString());

    httpClient.stop();
  }
	
  private static String getFileList() {

    JsonObject jsonObj = new JsonObject();
        
    // 파일 타입 
    jsonObj.addProperty("type", "txt");

    // 파일 목록
    File directory = new File("./src/main/resources/dir-exam");
    File[] fileList = directory.listFiles();
        
    JsonArray jsonArr = new JsonArray();
    for (File file : fileList) {
      jsonArr.add(file.getName());
    }
    jsonObj.add("files", jsonArr);
        
    String res = jsonObj.toString();
    return res; 
  }
}
```

* * *

### [References]
1. N/A
