## Matrix 회전하기

목차

1. [공통 출력 로직](#공통-출력-로직)
1. [Matirix 회전하기](#matirix-회전하기)

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
    System.out.println("*** 시계방향 90도 회전 ***");
    int rotateArr90[][] = rotate90(arr);
    for (int idx = 0; idx < rotateArr90.length; idx++) {
      System.out.println(Arrays.toString(rotateArr90[idx]));
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

### Matirix 회전하기

#### 1. 시계방향으로 90도 회전하기

- 코드

```java
public static int[][] rotate90(int inArray[][]) {

  // 규칙: array[row][col] = array[col][n-1-row]
  // ex) [0.0][0.1][0.2]      [2.0][1.0][0.0]
  //     [1.0][1.1][1.2]  =>  [2.1][1.1][0.1]
  //     [2.0][2.1][2.2]      [2.2][1.2][0.2]

  int rowNum = inArray.length;
  int colNum = inArray[0].length;

  // row와 col 이 바뀌어야 함
  int rotatedArr[][] = new int[colNum][rowNum];
  for (int row = 0; row < rowNum; row++) {
    for (int col = 0; col < colNum; col++) {
      rotatedArr[col][rowNum-1-row] = inArray[row][col];
    }
  }

  return rotatedArr;
}
```

- 실행 결과

> [16, 12, 8, 4, 0]  
[17, 13, 9, 5, 1]  
[18, 14, 10, 6, 2]  
[19, 15, 11, 7, 3]  


#### 2. 시계방향으로 90도 회전하기

- 90도 회전을 2회 수행

* * *

### [References]
1. N/A
