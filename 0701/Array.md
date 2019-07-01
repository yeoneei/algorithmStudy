# Array

## C++ 에서 배열의 크기
- c++ 배열은 크기 정보가 없다
```
int average (int a[], int n)
int average (int *a, int n)
```


## 다차원 배열
- 다차원 배열의 정의
    - 인덱스연사자를 차원수만큼 쓴다
- arr[3][3]에서 arr[0], arr[1], arr[2]는 각각 세개짜리 배열을 가르킨다


## 함수에서 다차원 배열 사용
```
int average (int m[][3]);
int average (int *m, int n1, int n2); //n1, n2는 크기
```
```
int arr[3][4][2];
int function(int t[][4][2]){
    ...
}
int function2(int *t, int n1, int, n2, int n3)//n1, n2, n3는 각 배열 크기
r = function(arr);
r = function2(arr, 3,4,2);
```



