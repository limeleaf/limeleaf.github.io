## 순열과 조합

목차

1. [순열과 조합](#순열과-조합)

* * *

### 순열과 조합

- 코드
```Java
public class NumberOfCasesTest {

	public static List<String> permutationResult = new ArrayList<String>();
	public static Set<String> combinationResultSet = new TreeSet<String>();

	public static void main(String[] args) {
		//char[] charArr = { 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M' };
		char[] charArr = { 'A', 'B', 'C'};

		// 순열
		permutation(charArr, 0, 2);

		// 조합
		combination(charArr, 0, 2);

		System.out.println("순열");
		Collections.sort(permutationResult);
		for (int idx = 0; idx < permutationResult.size(); idx++) {
			System.out.println(permutationResult.get(idx));
		}

		System.out.println("조합");
		Iterator<String> itr = combinationResultSet.iterator();
		while(itr.hasNext()) {
			System.out.println(itr.next());
		}
	}

	public static void permutation(char[] arr, int depth, int count) {

		if (depth == count) {
			permutationResult.add(Arrays.toString(Arrays.copyOfRange(arr, 0, count)));
			return;
		}

		for (int i = depth; i < arr.length; i++) {
			swap(arr, i, depth);
			permutation(arr, depth + 1, count);
			swap(arr, i, depth);
		}
	}

	public static void swap(char[] arr, int i, int j) {
		char temp = arr[i];
		arr[i] = arr[j];
		arr[j] = temp;
	}

	public static void combination(char[] arr, int depth, int count) {

		if (depth == count) {
			char[] tmpArray = Arrays.copyOfRange(arr, 0, count);
			Arrays.sort(tmpArray);

			boolean flag = false;
			Iterator<String> itr = combinationResultSet.iterator();
			while(itr.hasNext()) {
				if(itr.next().equals(Arrays.toString(tmpArray))) {
					flag = true;
				}
			}
			if(!flag) {
				combinationResultSet.add(Arrays.toString(tmpArray));
			}

			return;
		}

		for (int i = depth; i < arr.length; i++) {
			swap(arr, i, depth);
			combination(arr, depth + 1, count);
			swap(arr, i, depth);
		}
	}
}
```

- 실행 결과
> 순열  
[A, B]  
[A, C]  
[A, D]  
[B, A]  
[B, C]  
[B, D]  
[C, A]  
[C, B]  
[C, D]  
[D, A]  
[D, B]  
[D, C]  

> 조합  
[A, B]  
[A, C]  
[A, D]  
[B, C]  
[B, D]  
[C, D]  

* * *

### [References]
1. N/A
