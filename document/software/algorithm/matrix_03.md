## Matrix 대칭변환하기

목차

1. [공통 출력 로직](#공통-출력-로직)
1. [Matirix 대칭변환하기](#matirix-대칭변환하기)

* * *

### 공통 출력 로직

- 코드

```java
public class MatrixTest01 {
  public static void main(String[] args) {

    int rowNum = 5;
		int colNum = 4;

		// 초기 데이터 세팅
		System.out.println("*** 초기 값 ***");
		int arr[][] = new int[rowNum][colNum];
		int count = 0;
		for (int row = 0; row < rowNum; row++) {
			for (int col = 0; col < colNum; col++) {
				arr[row][col]=count;
				count++;
			}
		}
		for (int idx = 0; idx < arr.length; idx++) {
			System.out.println(Arrays.toString(arr[idx]));
		}

		// (1) 시계 방향으로 90도 회전
		int result[][] = method(arr);
		for (int idx = 0; idx < result.length; idx++) {
			System.out.println(Arrays.toString(result[idx]));
		}
  }
}
```

- 초기값

> [0, 1, 2, 3]  
[4, 5, 6, 7]  
[8, 9, 10, 11]  
[12, 13, 14, 15]  
[16, 17, 18, 19]  

* * *

### Matirix 대칭변환하기

#### 1. m X n Matrix 대칭 규칙

- 대각선 대칭: array[col][row] = array[row][col]
- 상하 대칭: array[row][col] = array[col][m-1-row]
- 좌우 대칭: array[row][col] = array[row][n-1-col]

#### 2. 구현

- 코드

```java
public static int[][] symmetric(int inArray[][], int type) {

  int rowNum = inArray.length;
  int colNum = inArray[0].length;
  int resultArr[][] = null;

  // 대각선 대칭
  if(type == 1) {
    resultArr = new int[colNum][rowNum]; // row와 col 이 바꿔야 함
    for (int row = 0; row < rowNum; row++) {
      for (int col = 0; col < colNum; col++) {
        resultArr[col][row] = inArray[row][col];
      }
    }
  // 좌우 대칭
  } else if (type == 2){
    resultArr = new int[rowNum][colNum];
    for (int row = 0; row < rowNum; row++) {
      for (int col = 0; col < colNum; col++) {
        resultArr[row][colNum-1-col] = inArray[row][col];
      }
    }
  // 상하 대칭
  } else if (type == 3){
    resultArr = new int[rowNum][colNum];
    for (int row = 0; row < rowNum; row++) {
      for (int col = 0; col < colNum; col++) {
        resultArr[rowNum-1-row][col] = inArray[row][col];
      }
    }
  }

  return resultArr;
}
```

- 실행 결과(대각선 대칭)

> *** 대각선 대칭 ***  
[0, 4, 8, 12, 16]  
[1, 5, 9, 13, 17]  
[2, 6, 10, 14, 18]  
[3, 7, 11, 15, 19]  

- 실행 결과(좌우 대칭) 

> [3, 2, 1, 0]  
[7, 6, 5, 4]  
[11, 10, 9, 8]  
[15, 14, 13, 12]  
[19, 18, 17, 16]  

- 실행 결과(상하 대칭)

> [16, 17, 18, 19]  
[12, 13, 14, 15]  
[8, 9, 10, 11]  
[4, 5, 6, 7]  
[0, 1, 2, 3]  

* * *

### [References]
1. N/A
