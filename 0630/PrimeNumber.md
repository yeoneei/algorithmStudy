# 소수 

## 목차
- 소수판별
- 에라토스테네스 체

## 소수 판별법
- 소수(Prime Number)란?
    - 1과 자기자신외에 나누어 떨어지는 정수가 없는 양의 정수
    - 2, 3, 5, 7, 11, 13...
- N이 소수인지 아닌지 판단하는 법
    1. 2 ~ N-1 까지의 정수로 나누어 보는 방법 - O(n)
    2. 1 ~ sqrt(N)까지의 정수로 나누어 보는 방법 - O(n<sup>0.5</sup>)
        - ex) 12 = 2 * 6 = 3 * 4 = 4 * 3 = 6 *2

## 에라토스테네스 체
- 주어진 N보다 작은 모든 소수를 구한다
- 배수들을 다 지운다
- ex) 120까지의 모든 소수를 구한다  
        2를 제외한 모든 2의 배수를 체크한다  
        3을 제외한 모든 3의 배수를 체크한다  
        ...  
        체크가 안된 수들이 소수다

## 코드
```
void primNumber(int n){
    bool *arr = new bool[n+1];

    for(int i=0; i< n+1; i++){
        arr[i] = true;
    }

    for(int i=2; i<n+1;i++){
        if(arr[i]){
            for(int j= i+i; j<n+1;j+=i){
                arr[j]=false;
            }
        }
    }

    for(int i=2; i<n+1 ;i++){
        if(arr[i]!=0){
            cout<<i;
        }
    }
}
```
