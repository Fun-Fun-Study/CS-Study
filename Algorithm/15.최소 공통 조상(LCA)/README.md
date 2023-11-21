## 🔎 최소 공통 조상 (LCA, Lowest Common Ancestor)

최소 공통 조상은 **트리 구조**에서 임의의 두 정점이 갖는 **가장 가까운 조상 정점**을 의미한다.

![image (85)](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/903f2ce2-3515-48d6-8891-2468dffe3024)

예시 트리

위와 같은 예시 트리 구조에서, **13, 15번 정점의 최소 공통 조상은 5번 정점**이 된다. 마찬가지로,

![image (86)](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/253e5544-d5b9-424b-bf12-1736f65c34b1)

**13, 11번 정점의 최소 공통 조상은 1번** 정점(Root)이 된다.

### LCA를 선형 탐색으로 구하기 : O(Depth)

트리에서 이러한 최소 공통 조상을 찾으려면 어떤 방식을 사용해야 할까?

가장 단순한 방법으로는, 두 포인터를 두고 **가리키는 정점이 같아질 때까지 부모 노드로 거슬러 올라가면** 될 것이다.

즉 Parent[x]를 정점 x의 부모 노드라 할 때, **x = Parent[x]** 연산을 반복하면 될 것이다.

![image (87)](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/5d8814dd-becf-4c3e-964d-da4d5404eb5a)

하지만 구하고자 하는 **두 정점의 LEVEL(깊이)이 다르다면 문제가 발생**한다.

11, 13번 정점의 최소 공통 조상을 찾는 상황을 생각해보자.

13번 정점에서 최소 공통 조상인 1번 정점까지는 4번을 거슬러 올라가야 하지만,

11번 정점에서는 3번을 거슬러 올라가면 도달할 수 있기 때문이다.

잠시 다른 예를 들어, **13번과 15번 정점의 최소 공통 조상**을 구해보자. 최소 공통 조상은 5번 정점이다.

![image (88)](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/8b8b4c5d-8311-4e94-9aaa-6dfe69bbd47f)

![image (89)](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/e6a59a75-bc64-433a-a818-b3e3f1416709)

동시에 거슬러 올라간다면 원래 13번 정점을 가리키던 포인터가 5번 정점까지 도달한 순간,

원래 15번 정점을 가리키던 포인터는 2번 정점을 가리키게 된다.

따라서 동시에 거슬러 올라가기 전, **두 정점의 깊이를 동일하게 맞춰야 한다**.

![image (90)](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/4b78ca48-6701-4d2f-9631-36224507e7fa)

다시 원래 문제로 돌아와서, 깊이를 맞춘 후 이제는 **9번, 11번 정점의 최소 공통 조상을 구하는 문제**로 바뀌었다.

두 정점의 깊이가 같기 때문에, **가리키는 정점이 같아질 때까지 동시에 거슬러 올라가면** 된다.

![image (91)](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/bc754ece-01b9-4514-b3c0-54c9a0cbdd77)

**출처**

---

[최소 공통 조상 (LCA, Lowest Common Ancestor)](https://4legs-study.tistory.com/121)

**백준**

---

[11437번: LCA](https://www.acmicpc.net/problem/11437)

**더 자세히**

---

[LCA(Lowest Common Ancestor) 알고리즘](https://www.crocus.co.kr/660)