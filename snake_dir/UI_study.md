# UI Study #

## 1. Cursor 없애기

```
void cursor(int n){  // 커서 보이기 & 숨기기
    HANDLE hConsole;
    CONSOLE_CURSOR_INFO ConsoleCursor;
 
    hConsole = GetStdHandle(STD_OUTPUT_HANDLE);
 
    ConsoleCursor.bVisible = n;
    ConsoleCursor.dwSize = 1;
 
    SetConsoleCursorInfo(hConsole , &ConsoleCursor);
}

void main(){
    cursor(0); // cursor(0);은 커서 숨기기, cursor(1);은 커서 보이기
}

출처: https://www.crocus.co.kr/38 [Crocus]
```

## 2. Console 글자에 색깔 넣기

```
#include <Windows.h>

SetConsoleTextAttribute( GetStdHandle( STD_OUTPUT_HANDLE ), 해당번호);
[출처] C언어 콘솔에 글자색 넣기|작성자 Marbong
```
위의 함수를 쓰려면 <Windows.h> 헤더가 필요하고 색깔은 다음 중에서 고르면 된다.

검정 | 파랑 | 초록 | 옥색 | 빨강 | 자주 | 노랑 | 흰색 | 회색
-----|-----|------|------|-----|------|------|-----|-----
  0  |  1  |  2   |  3   |  4  |  5   |  6   |  7  |  8

연한파랑 | 연한초록 |연한옥색 | 연한빨강 | 연한자주 | 연한노랑 | 진한흰색
--------|---------|---------|---------|---------|----------|---------
   9    |    10   |   11    |    12   |   13    |    14    |    15


## 3. Sleep

<Windows.h> 헤더를 추가하고 Sleep(time) 을 사용하면 그동안 멈췄다가 시작  
time 기준은 ms였던거같다


## 4. Console에 위치 지정해서 문자 띄우기

gotoxy함수를 이용해서 하는데 우선 <Windows.h> 헤더를 선언하고 시작하자.  

```
void gotoxy(int x,int y){
    COORD pos={y,x};
    SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE),pos);
}
```

위 함수는 console창에서 i번째 줄 j번째 열로 커서를 이동하라는 함수야  
이동한 다음에 printf등을 통해서 문자를 덮어써주면 되  
예시코드 보면 바로 알듯  

```
int val = 0, n=10;
// initial screen
for(int i=0; i<n; i++){
    for(int j=0; j<n; j++){
        printf("%d", val);
    }
    printf("\n");
}
while(1){
    val^=1;
    for(int i=0; i<n; i++){
        for(int j=0; j<m; j++){
            gotoxy(i, j); printf("%d", val);
            Sleep(100);
        }
    }
}
```
