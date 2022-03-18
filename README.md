# Algorithm-Study(2022 1st semester)
## 1st Week
### 1. 창고다각형([백준 2304번][2304Link])
[2304Link]: https://www.acmicpc.net/problem/2304

#### 풀이과정
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
<br/>

#### 결과
![2304 result](https://user-images.githubusercontent.com/89967066/158008710-b73e62d9-e939-4eba-b3c4-d965541e34c4.png)
***
<br/>
<br/>

### 2. 오큰수([백준 17298번][17298Link])
[17298Link]: https://www.acmicpc.net/problem/17298
#### 풀이과정
단순히 이중 for문을 통해서 구현한 결과, 38%에서 시간초과 오류 발생.

![17298 try](https://user-images.githubusercontent.com/89967066/158008818-cf7e8b9d-6add-48ca-8454-f8fa60ae4458.png)
<br/>
<br/>

그러던 중 문제 카테고리가 스택임을 고려하였으나, 단순히 특정 숫자를 스택에 넣을 경우, 위의 이중 for문과 마찬가지로 O(N^2)의 시간복잡도를 갖을 거라 생각

![17298 way](https://user-images.githubusercontent.com/89967066/158010187-efa14767-9b3a-4258-b01a-8243fa586067.png)

그 후 단순히 숫자를 스택에 넣는 것이 아닌, 해당 숫자의 index(비교하는 숫자)를 스택에 넣어보는 것을 떠올리면서, 해당 스택에 들어간 index를 가리키는 숫자보다 큰 경우, 
결과 값을 해당 값으로 출력하는 방식을 떠올림.


이에 따라, 처음에 입력받은 수 만큼의 크기를 갖는 -1이 입력된 리스트를 만든 후, 입력받은 수들의 index를 스택에 저장.
저장된 index에 대해서, 해당 값보다 큰 수가 나올 경우, 스택에 들어있는 해당 index를 제거한 후, 큰 수를 -1이 저장된 리스트의 해당 index에 저장하는 방식을 떠올림
* * *

#### Python Code
    n = int(input())
    inf = list(map(int,input().split()))
    ans = [-1 for _ in range(n)]
    stack = []

    for i in range(n):
        while(stack and inf[stack[-1]] < inf[i]): #계속 쌓이는 경우는 감소되는 경우밖에 없음 따라서 제일 앞에보다 크면 나머지수도 큼
            ans[stack[-1]] = inf[i]
            stack.pop()
        stack.append(i)
    for i in ans:
        print(i, end=" ")
  
<br/>

#### 결과
![17298 res](https://user-images.githubusercontent.com/89967066/158010477-7c408912-cbcb-4e72-98a4-c51b605261c5.png)

***
<br/>
<br/>

## 2st Week
### 1. Z([백준 1074번][1074Link])
[2304Link]: https://www.acmicpc.net/problem/1074

#### 풀이과정
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
<br/>
