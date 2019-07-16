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
int array[3][3]
int average (int m[][3]);
int average (int *(m[3]),int n);
int average3 (int *m, int n1, int n2); //n1, n2는 크기

r = average(array);
r = average3(&array[0][0],3,3);


```
```
int arr[3][4][2];
int function(int t[][4][2]){    
    ...
}
int function2(int *t, int n1, int, n2, int n3)//n1, n2, n3는 각 배열 크기
r = function(arr);
r = function2(&arr[0][0][0], 3,4,2);
```
## 미로의 표현과 그리기
- 미로의 표현
    - 2차원 배열로 표현한다.
    - 0은 길, 1은 벽
```
enum{
    UP = 1,
    RIGHT = 2,
    DOWN = 4, 
    LEFT =8,
};
```
- [0][0][1][1] : 배열에서 이러면 DOWN과 LEFT로 가는것 중복해서 사용할 수 있음 
    - 여러 방향을 표시할 수 있음!
```
int CMaze::GetShape(int x, int y){
    int shape =0;
    if(m_arrayMax[y][x]!=0){ //벽이 있는 경우에만 경우의 수를 따진다
        if(y>0 && m_arrayMaze[y-1][x])
            shape|=UP;//위쪽에 벽이 있나
        if(y < MAX_SIZE-1 && m_arrayMaze[y+1][x])
            shape|=DOWN; //아래쪽에 벽이 있나
        if(x > 0 && m_arrayMax[y][x-1])
            shape|=LEFT; //왼쪽에 벽이 있나
        if(x<MAX_SIZE-1 && m_arrayMaze[y][x+1])
            shape|=RIGHT; //오른쪽에 벽이있나
    }
    return shape;
}
```

## 미로 탐색 알고리즘 : 우선법
- Right Handl On Wall (우선법)
    - 갈림길을 만났을 때 우선적으로 오른쪽으로 간다
    - 오른쪽에 손을 대고 가기 
```
while(Stil_In_Maze){
    Turn_Right;
    while(Wall_Ahead){
        Turn_Left;
    }
    Go_Forwared;
}
```
- 기본 함수들
```
void CMaze::GoForward(int &x, int &y, int dir){
    x = (dir == LEFT ? --x : dir==RIGHT? ++x : x);
    y = (dir == UP ? --y : dir == DOWN ? ++y : y);
}
void CMaze::StillInMaze(int x, inty){
    if(x>0 && x<MAZE_SIZE-1 && y>0 && y < MAZE_SIZE-1){
        return true;
    }else{
        return false;
    }
}
bool CMaze::WallAhead(int x, int y, int dir){
    x = (dir == LEFT ? --x : dir==RIGHT? ++x : x);
    y = (dir == UP ? --y : dir == DOWN ? ++y : y); 
    return m_arrayMaze[y][x]!=0; 
}
void CMaze::TrunLeft(int &dir){
    dir >>=1;
    dir = ( dir==0? LEFT:dir);
}
void CMaze::TrunRight(int &dir){
    dir <<=1;
    dir = (dir> LEFT? UP:dir);
}
void CMaze::RightHandOnWall(int x, int y, int dir){
    while(StillInMaze(x,y)){
        Turn Right(dir);
        while(WallAhead(x,y,dir)){
            TurnLeft(dir);
        }
        GoForWard(x,y,dir);
    }
}
```
## 최단경로 찾기
- 우선법 진행과정의 좌표 리스트를 저장
- 저장된 좌표리스트에서 중복되는 좌표부분 잘라냄




