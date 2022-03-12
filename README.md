# Algorithm-Study
## 1st Week
### 1. 창고다각형([백준 2304번][2304Link])
[2304Link]: https://www.acmicpc.net/problem/2304

### 풀이과정
<br/>

![2304 input](https://user-images.githubusercontent.com/89967066/158007696-cffb0193-e537-41fe-9e1b-8bb1b1eaa7f3.png)
<br/>
입력 데이터를 어떤 식으로 받을지 고민을 하다, 문제에서 N과 L이 모두 1000이하이므로, 공간이 1000인 빈 리스트를 만들어 입력받은 L값에 해당되는 index에 해당 높이를 넣는 방식으로 데이터를 저장.
<br/>
<br/>

![2304 graph](https://user-images.githubusercontent.com/89967066/158007765-176a5448-1b93-4f22-bb58-6a76c1f95b2b.png)
<br/>
이후 최고 높이를 기준으로, 왼쪽부분은 index를 증가시키면서 더하는 걸로, 오른쪽은 index를 감소시키면서 더하는 방식을 생각
<br/>
<br/>

![2304 exa](https://user-images.githubusercontent.com/89967066/158008418-7728c038-2cd0-49aa-ba8e-a2f2aaaf31cf.jpg)
<br/>
여기서, 최고높이가 한개가 아닌 여러 개인 경우를 생각. 따라서 데이터를 받는 과정에서, 최고 높이가 같은 경우, 해당 인덱스를 저장하는 리스트를 하나 만들어서 저장하고, 기존  최대 높이보다
더 큰 경우 리스트를 초기화 하는 방식을 생각

높이를 더하는 과정에서 n값이 1000이하이므로, 그냥 for문을 통해서 구현하기로 결정.

* * *

#### Python Code

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
  
***

### 2. 오큰수([백준 17298번][17298Link])
[17298Link]: https://www.acmicpc.net/problem/17298
