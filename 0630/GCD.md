# 최대공약수 ( GCD )
## 최대공약수 (Greatest Common Divisor)
- 주어지는 두 정수의 약수중에서 가장 큰 공통 약수
- 280과 30의 GCD는 10이다
- 소인수분해를 통해 GCD를 구할 수 있다 

## GCD와 관련된 법칙
- GCD(u,v) = GCD(u-v, v) if(u > v)
- GCD(u,v) = GCD(v, u)
- GCD(u,0) = u

## GCD 구하기
임의의 두 정수 u, v에 대해  
(1) v가 u보다 크다면 v와 u의 값을 바꾼다  
(2) u = u-v  
(3) u가 0이 이면 v가 최대공약수, 0이아니면 (1)로 돌아간다

## 구현
```
int get_gcd(int u, intv){
    int t;
    while(u){
        if(u < v){
            t = u; u = v; v= t;
        }
        u = u-v;
    }
    return v;
}
```

## GCD의 개선
- 뺄셈기반은 u, v가 차이가 많이 날 떄 많은 반복을 한다
- 뺄셈 == 나눗셈의 나머지
    - GCD(u, v) == GCD (u%v, v) == GCD(v, u%v)
    - u%v < v
```
int gcd_recursive(int u, int v){
    if(v==0){
        return u;
    }
    else
        return gcd_return(v, u%v);
}
```

