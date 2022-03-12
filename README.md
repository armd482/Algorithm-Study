# Algorithm-Study
## 1st Week
### 1. 창고다각형([백준 2304번][2304Link])
[2304Link]: https://www.acmicpc.net/problem/2304

* * *
접근 방법
* * *
1. 이중 for문을 이용한 n^2

Python Code

    max_num = 0 # 최고 높이를 구하기 위한 변수 설정
    max_loc = [] #최고 높이를 갖는 index값들 저장
    info = [[] for _ in range(1001)]
    ans = 0 # 최종 합계를 구할 변수 설정
    end = 0 # 입력된 index값 중 가장 큰 값(가장 끝 index)

    n = int(input())
    for _ in range(n):
        a,b = map(int,input().split())
        info[a].append(b)
        if(end < a): #입력된 index값이 가장 큰 경우
            end = a
        if(max_num < b): # 높이가 가장 큰 경우
            max_num  = b
            max_loc = [a] # 기존 index를 저장한 리스트 초기화
        elif(max_num == b): # 최고높이가 여러 개인 경우
            max_loc.append(a)
        
    val = 0
    min_index = min(max_loc)
    max_index = max(max_loc)
    for i in range(1,min_index):
        if(info[i] and val < info[i][0]):
            val = info[i][0]
        ans += val
    
    ans += max_num * (max_index - min_index + 1)

    val = 0
    for i in range(end, max_index,-1):
        if(info[i] and val < info[i][0]):
            val = info[i][0]
        ans += val
    print(ans)
  

