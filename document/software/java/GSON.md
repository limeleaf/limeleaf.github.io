## Java Thread

목차

1. [Gson](#Gson)

* * *

### GSON

#### 1. GSON을 활용한 JSON Data Handling 예제

- 기본적인 사용법
```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.util.List;

import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonArray;
import com.google.gson.JsonElement;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;
import com.google.gson.reflect.TypeToken;

import gson.Response.Item;
import gson.Response.Items;

/**
 * Hello world!
 *
 */
public class GsonConverter {

    public static void main( String[] args ) throws Exception {

    	// Json String
      String jsonData = readJsonStr();

      // Gson gsonBasic = new Gson(); // 기본 
      Gson gson = new GsonBuilder().setPrettyPrinting().create(); // 기본(+ 예쁘게 출력) 
      Gson gsonWithNull = new GsonBuilder().setPrettyPrinting().serializeNulls().create(); // null인 프로퍼티도 출력  
        
      // Element 추출 
      JsonParser parser = new JsonParser();
      JsonElement element = parser.parse(jsonData);
        
      // JsonObject 추출 
      JsonObject rootJsonObject = element.getAsJsonObject().get("response").getAsJsonObject();
      JsonObject bodyJsonObject = rootJsonObject.getAsJsonObject().get("body").getAsJsonObject();
      JsonObject itemsJsonObject = bodyJsonObject.getAsJsonObject().get("items").getAsJsonObject();  
        
      // Case-01) 전체 데이터를 하나의 VO로 만들
      Response responeVo = gson.fromJson(rootJsonObject, Response.class);
        
      // Case-02) Data 일부를 List<VO>형으로 변환
      JsonArray itemArray = itemsJsonObject.getAsJsonObject().get("item").getAsJsonArray();
      List<Item> ItemList = gson.fromJson(itemArray.toString(), new TypeToken<List<Item>>(){}.getType());

      // Case-03) Data 일부를 VO로 변환
      Items itemsVo = gson.fromJson(itemsJsonObject, Items.class);
		
      // Case-04) Data를 String으로 변환 - null인 값은 출력 안됨  
      String resultJsonStr = gson.toJson(itemsVo);
      System.out.println(resultJsonStr);		
      System.out.println("========================");
		
		  // Case-05) Data를 String으로 변환 - null인 값도 출력됨  
      String resultJsonStrWithNull = gsonWithNull.toJson(itemsJsonObject);
      System.out.println(resultJsonStrWithNull);
      System.out.println("========================");

      System.out.println("끝!!");
    }

    public static String readJsonStr() throws Exception {
        
      String result = "";

      /*
        File a = new File("./");
        System.out.println(a.getAbsolutePath());
        System.out.println(a.getPath());
      */
        
      BufferedReader br = new BufferedReader(new FileReader("./src/main/resources/json-data-01.txt"));	
    
      String line = null;
      while((line = br.readLine()) != null) {
        //System.out.println(line);
        result = result + line;
      }
      br.close();
      
      return result;
    }
}
```

- Json Data 처리용 VO
```java
import java.util.List;

public class Response {

  private Header header;
  private Body body;
	
  // Setter/Getter
  public Header getHeader() {
    return header;
  }

  public void setHeader(Header header) {
    this.header = header;
  }

  public Body getBody() {
    return body;
  }

  public void setBody(Body body) {
    this.body = body;
  }

  // Header 클래스
  public static class Header {
		
    String resultCode;
    String resultMsg;
		
    public String getResultCode() {
      return resultCode;
    }
    public void setResultCode(String resultCode) {
      this.resultCode = resultCode;
    }
    public String getResultMsg() {
      return resultMsg;
    }
    public void setResultMsg(String resultMsg) {
      this.resultMsg = resultMsg;
    }	
  }
	
  // Body 클래스 
  public static class Body {
		
    // 아이템 목록 객체
    private Items items;

    public Items getItems() {
      return items;
    }

    public void setItems(Items items) {
      this.items = items;
    }
  }
	
  // 아이템 목록 클래스
  public static class Items {
		
    private List<Item> item;
    
    public List<Item> getItem() {
      return item;
    }

    public void setItem(List<Item> item) {
      this.item = item;
    }
  }
	
  // 아이템 클래스
  public static class Item {
		
    private String name; // 제품 이름
    private String id; // ID
    private String year; // YEAR
    private String code; // 코드
		
    public String getName() {
      return name;
    }
    public void setName(String name) {
      this.name = name;
    }
    public String getId() {
      return id;
    }
    public void setId(String id) {
      this.id = id;
    }
    public String getYear() {
      return year;
    }
    public void setYear(String year) {
      this.year = year;
    }
    public String getCode() {
      return code;
    }
    public void setCode(String code) {
      this.code = code;
    }
  }
}
```

* * *

### [References]
1. N/A
