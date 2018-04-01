## Matrix 채우기

목차

1. [공통 출력 로직](#공통-출력-로직)
1. [달팽이 알고리즘](#달팽이-알고리즘)
1. [지그재그로 채우기](#지그재그로-채우기)
1. [대각선 방향으로 채우기](#대각선-방향으로-채우기)

* * *

### 공통 출력 로직

```Java
public class MatrixTest01 {
  public static void main(String[] args) {

    int rowNum = 3;
    int colNum = 4;

    int arr[][] = method(rowNum, colNum);
    for (int idx = 0; idx < arr.length; idx++) {
      System.out.println(Arrays.toString(arr[idx]));
    }
  }
}
```

* * *

### 달팽이 알고리즘

#### 1. 시계 방향으로 돌면서 채우기

- 코드
```java
public static int[][] rightSnail(int rowNun, int colNum) {

  int result[][] = new int[rowNun][colNum];

  int startRow = 0;
  int endRow = rowNun - 1;
  int startCol = 0;
  int endCol = colNum - 1;

  int value = 1;

  // Row 수 만큼 반복
  for (int idx = 0; idx < rowNun; idx++) {
    // 짝수 회차에는 "왼쪽=>오른쪽", "위=>아래"로 진행됨
    if (idx % 2 == 0) {
      // 욑쪽 -> 오른쪽
      for (int jdx = startCol; jdx <= endCol; jdx++) {
        result[startRow][jdx] = value;
        value++;
      }
      startRow++;

      // 위 -> 아래
      for (int jdx = startRow; jdx <= endRow; jdx++) {
        result[jdx][endCol] = value;
        value++;
      }
      endCol--;

    // 홀수 회차에는 "오른쪽=>왼쪽", "아래=>위"로 진행됨
    } else {
      // 오른쪽 -> 왼쪽
      for (int jdx = endCol; jdx >= startCol; jdx--) {
        result[endRow][jdx] = value;
        value++;
      }
      endRow--;

      // 아래 -> 위
      for (int jdx = endRow; jdx >= startRow; jdx--) {
        result[jdx][startCol] = value;
        value++;
      }
      startCol++;
    }
  }
  return result;
}
```

- 실행 결과
> [1, 2, 3, 4]
[10, 11, 12, 5]
[9, 8, 7, 6]


#### 2. 반시계 방향으로 돌면서 채우기

- 코드
```Java
public static int[][] leftSnail(int rowNun, int colNum) {

  int result[][] = new int[rowNun][colNum];

  int startRow = 0;
  int endRow = rowNun - 1;
  int startCol = 0;
  int endCol = colNum - 1;

  int value = 1;

  // Row 수 만큼 반복
  for (int idx = 0; idx < rowNun; idx++) {
    // 짝수 회차에는 "위=>아래", "왼쪽=>오른쪽"으로 진행됨
    if (idx % 2 == 0) {
      // 위 -> 아래
      for (int jdx = startRow; jdx <= endRow; jdx++) {
        result[jdx][startCol] = value;
        value++;
      }
      startCol++;

      // 욑쪽 -> 오른쪽
      for (int jdx = startCol; jdx <= endCol; jdx++) {
        result[endRow][jdx] = value;
        value++;
      }
      endRow--;

    // 홀수 회차에는  "아래=>위", "오른쪽=>왼쪽"으로 진행됨
    } else {
      // 아래 -> 위
      for (int jdx = endRow; jdx >= startRow; jdx--) {
        result[jdx][endCol] = value;
        value++;
      }
      endCol--;

      // 오른쪽 -> 왼쪽
      for (int jdx = endCol; jdx >= startCol; jdx--) {
        result[startRow][jdx] = value;
        value++;
      }
      startRow++;
    }
  }

  return result;
}
```

- 실행 결과
> [1, 10, 9, 8]
[2, 11, 12, 7]
[3, 4, 5, 6]

* * *

### 지그재그로 채우기

- 코드
```Java
public static int[][] zigzag(int rowNun, int colNum) {

  int result[][] = new int[rowNun][colNum];

  int startCol = 0;
  int endCol = colNum - 1;

  int value = 1;

  // Row 수 만큼 반복
  for (int row = 0; row < rowNun; row++) {
    if (row % 2 == 0) {
      // 오른쪽으로 이동
      for (int idx = startCol; idx <= endCol; idx++) {
        result[row][idx] = value;
        value++;
      }

    } else {
      // 왼쪽으로 이동
      for (int idx = endCol; idx >= startCol; idx--) {
        result[row][idx] = value;
        value++;
      }
    }
  }

  return result;
}
```

- 실행 결과
> [1, 2, 3, 4]
[8, 7, 6, 5]
[9, 10, 11, 12]

* * *

### 대각선 방향으로 채우기

- 코드
```Java
public static int[][] diagonal(int rowNum, int colNum) {

  int result[][] = new int[rowNum][colNum];

  int value = 1;
  int totalCount = rowNum + (colNum -1);

      // 대각선 개수
      for(int idx=0; idx<totalCount; idx++){
        // row 수 만큼 매번 반복한다
          for(int row=0; row<rowNum; row++){
            // idx의 증가만큼 col도 증가, row가 증가한 만큼 col은 감소
              int col = idx - row;
              // col이 사용 범위에 있는 경우에만 숫자 지정
              if(col >= 0 && col < colNum){
                  result[row][col] = value;
                  value++;
              }
          }          
      }

  return result;
}
```

- 실행 결과
> [1, 2, 4, 7]
[3, 5, 8, 10]
[6, 9, 11, 12]

* * *

### [References]
1. N/A
