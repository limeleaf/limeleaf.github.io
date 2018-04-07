## 괄호 확인 알고리즘

목차

1. [괄호 확인 알고리즘](#괄호-확인-알고리즘)

* * *

### 괄호 확인 알고리즘

- 코드

```java
public class PairCheckTest {

	public static void main(String[] args) {

		Stack<Character> pairStack = new Stack<Character>();

		String str = "[{name:\"name01\",age:1},{name:\"name02\", age:2}]";

		char[] array = str.toCharArray();

		for (int idx = 0; idx < array.length; idx++) {
			char ch = array[idx];
			if ((ch == '{') || (ch == '[')) {
				pairStack.push(ch);
				System.out.println("\"" + ch + "\" 괄호가 발견되어 \"" + ch + "\" 괄호 push");
			} else if ((ch == '}') || (ch == ']')) {
				char pop = pairStack.pop();
				System.out.println("\"" +ch + "\" 괄호가 발견되어 \"" + pop + "\" 괄호 pop");
			}
		}
	}
}
```

- 실행 결과  

> "[" 괄호가 발견되어 "[" 괄호 push  
"{" 괄호가 발견되어 "{" 괄호 push  
"}" 괄호가 발견되어 "{" 괄호 pop  
"{" 괄호가 발견되어 "{" 괄호 push  
"}" 괄호가 발견되어 "{" 괄호 pop  
"]" 괄호가 발견되어 "[" 괄호 pop  

* * *

### [References]
1. N/A
