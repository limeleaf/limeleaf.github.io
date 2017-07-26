## Pattern and Matcher

목차

1. [Pattern and Matcher](#pattern-and-matcher)

* * *

### Pattern and Matcher

#### 1. 정의 및 주요 특징

##### 1.1 Pattern

```
java.util.regex
Class Pattern

java.lang.Object
 java.util.regex.Pattern

All Implemented Interfaces:
Serializable
```

**A compiled representation of a regular expression.**
A regular expression, specified as a string, **must first be compiled** into an instance of this class. The resulting pattern can then be used to create **a Matcher object** that can match arbitrary character sequences against the regular expression. All of the state involved in performing a match resides in the matcher, so many matchers can share the same pattern.

##### 1.1 Matcher

```
java.util.regex
Class Matcher

java.lang.Object
 java.util.regex.Matcher

All Implemented Interfaces:
 MatchResult
```

An engine that performs match operations on a character sequence by interpreting a Pattern. **A matcher is created from a pattern by invoking the pattern's matcher method**. Once created, a matcher can be used to perform three different kinds of match operations:
- The **matches** method attempts to match <U>the entire input sequence</U> against the pattern.
- The **lookingAt** method attempts to match the <U>input sequence, starting at the beginning</U>, against the pattern.
- The **find** method scans <U>the input sequence looking for the next subsequence</U> that matches the pattern.




#### 2. 구현 예

1) 일반적인 사용 방법

```java
Pattern p = Pattern.compile("a*b");
Matcher m = p.matcher("aaaaab");
boolean b = m.matches();
```

2) Pattern 객체의 재사용 없이 matches 메소드를 수행하는 방법

> A matches method is defined by this class as a convenience for **when a regular expression is used just once**. This method compiles an expression and matches an input sequence against it in a single invocation.

```java
boolean b = Pattern.matches("a*b", "aaaaab");
```

#### 3. Summary of regular-expression constructs(주요 내용만)

#### 3.1 Character classes

| Construct  | Matcher |
| :------------ | :------------------- |
| [abc]	| 어떤 문자가, a나 b나 c인 경우 true (simple class) |
| [^abc]	| 어떤 문자가, a나 b나 c가 아닌 경우 true (negation) |
| [a-zA-Z]	| 어떤 문자가, 알파벳(대, 소문자)인 경우 true (range) |
| [a-d[m-p]]	| 어떤 문자가, a ~ d나 m ~ p 사이에 있는 경우: [a-dm-p] (union) |
| [a-z&&[def]]	| 어떤 문자가, 알파벳 소문자 이면서 d,e,f 인 경우 (intersection) |
| [a-z&&[^bc]]	| 어떤 문자가, 알파벳 소문자 이면서 b,c가 아닌 경우: [ad-z] (subtraction) |
| [a-z&&[^m-p]]	| 어떤 문자가, 알파벳 소문자 이면서 m~p 사이에 있지 않은 경우: [a-lq-z] (subtraction) |

#### 3.2 Predefined character classes

| Construct  | Matcher |
| :------------ | :------------------- |
| .	| Any character (may or may not match line terminators)	|
| \d	| A digit: [0-9]	|
| \D	| A non-digit: [^0-9]	|
| \s	| A whitespace character: [ \t\n\x0B\f\r]	|
| \S	| A non-whitespace character: [^\s]	|
| \w	| A word character: [a-zA-Z_0-9] |
| \W	| A non-word character: [^\w]	|

#### 3.3 Boundary matchers

| Construct  | Matcher |
| :------------ | :------------------- |
| ^	| The beginning of a line |
| $	| The end of a line |

#### 3.3 Greedy quantifiers

| Construct  | Matcher |
| :------------ | :------------------- |
| X?	| X가 하나거나 없음 |
| X*	| X가 0개 이상 |
| X+	| X가 최소 하나 이상 |
| X{n}	| X가 정확하게 n개 |
| X{n,}	| X가 최소 n개 |
| X{n,m}	| X가 최소 n개 최대 m개 |

#### 4. 주요 패턴

- 숫자 : ^[0-9]*$
- 영문자 : ^[a-zA-Z]*$
- 한글 : ^[가-힣]*$
- 영어 & 숫자 : ^[a-zA-Z0-9]*$
- E-Mail : ^[a-zA-Z0-9]+@[a-zA-Z0-9]+$
- 휴대폰 : ^01(?:0|1|[6-9]) - (?:\d{3}|\d{4}) - \d{4}$
- 일반전화 : ^\d{2.3} - \d{3,4} - \d{4}$
- 주민등록번호 : \d{6} \- [1-4]\d{6}
- IP 주소 : ([0-9]{1,3}) \. ([0-9]{1,3}) \. ([0-9]{1,3}) \. ([0-9]{1,3})

***

### [References]
1. <https://docs.oracle.com/javase/7/docs/api/>
1. <http://highcode.tistory.com/6>
