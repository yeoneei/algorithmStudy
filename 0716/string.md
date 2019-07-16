## 문자열 함수들 구현하기

### 주의
- 문자열 받을 때 C++11이상은 `char *name="yoeni"`이렇게 선언이 안됌
~~~
char str[100];
cin.getline(str,100,'\n');
cout<<strLen(str)<<endl;
~~~

### strlen
문자 길이 세는 함수
~~~
int strLen(char *str){
    int i=0;
    while(str[i]){
        i++;
    }
    return i;
}
~~~

### strcpy
문자열 복사 함수
~~~
void strCpy(char *des, char *src){
    int i=0;
    while((des[i]=src[i])){
        i++;
    }
}
~~~

### strcmp
문자열 비교 함수
~~~
int strCmp(const char *des, const char *src){
    int i=0;
    while(des[i]){
        if(des[i]!=src[i]){
            break;
        }
        i++;
    }
    return des[i]-src[i];
}
~~~

### strcat
문자열 이어 붙이기
~~~
void strcat(char *des, char *src){
    int i=0;
    while(des[i]){
        i++;
    }
    int j=0;
    while(src[j]){
        des[i]=src[j];
        i++;
        j++;
    }
}
~~~

### 문자열 뒤집기 
문자열 거꾸로 만들기
~~~
char* reverseStr(char *des){
    int i=0;
    while(des[i]){
        i++;
    }
    int end= i/2;
    for(int j=0;j<end;j++){
        char temp = des[j];
        des[j] = des[i-j-1];
        des[i-j-1]=temp;
    }
    return des;
}
~~~

## KMP 알고리즘

### 무식하게 찾기
- "I have a pen, I anve an apple"이라는 문장에서 "have"를 찾는 다고 하면 이중포문구조로 시간복잡도가 O(NM)이 되게 된다.
~~~
char str[100]="I have a apple, I have a pen";
char findStr[100]="have";

int size  = strLen(str);
int subSize = strLen(findStr);
for(int i=0; i<size-subSize;i++){
    bool find = true;
    for(int j=0; j<subSize;j++){
        if(str[i+j]!=findStr[j]){
            find=false;
            break;
        }
    }
    if(find) cout<<"position :"<<i<<"~"<<i+subSize-1<<endl;
}
~~~
### KMP란?
- 불일치가 발생한 텍스트 스트링의 앞 부분에 어떤 문자가 있는지를 미리 알고 있으므로, 불일치가 발생한 앞 부분에 대하여 다시 비교하지 않고 매칭을 수행
- 패턴을 전처리하여 배열 next[M]을 구해서 잘못된 시작을 최소화 한다
    - next[M] : 불일치가 발생했을 경우 이동할 다음 위치
- 시간 복잡도 : O(M+N);

~~~
void getPi(char *sub){
    int size= strLen(sub);
    int i=1,j=0;
    pi[0]=0;
    while(i<size){
        if(sub[i]==sub[j]){
            pi[i]=j+1;
            j++;
        }else{
            pi[i]=0;
            j=0;
        }
        i++;
    }
}

int kmp(char *pattern, char*sub){
    int pSize = strLen(pattern);
    int sSize = strLen(sub);
    
    int i=0,j=0;
    int count=0;
    for(i=0; i<pSize;i++){
        while(j>0 && pattern[i]!=sub[j]) j=pi[j-1];
        if(pattern[i]==sub[j]){
            if(j==sSize-1){
                result[count++]=i-sSize+1;
                j=pi[j-1];
            }else j++;
        }
    }
    return count;
    
}
~~~

## 보이어-무어
- 오른쪽에서 왼쪽으로 비교
- 대부분의 사용 소프트웨어에서 채택하고 있는 알고리즘
- 보이어-무어 알고리즘은 패턴에 오른쪽 끝에 이는 문자가 불일치 하고 이문자가 패턴 내에 존재하지 않는 경우, 이동 거리는 무려 패턴의 길이 만큼 된다

나중에 공부하고 추가하기!




