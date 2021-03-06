# 08. 트리(Tree)

## 08 - 1. 트리
**계층적 관계**를 **표현**하는 자료구조  


- 노드 `node`  
  : 트리를 이루는 요소
- 간선 `edge`  
  : 노드와 노드를 연결하는 연결선  
- 루트 노드 `root node`  
  : 최상위에 존재하는 노드
- 단말 노드(잎사귀 노드) `terminal node` `leaf node`   
  : 아래로 또 다른 노드가 연결되어 있지 않은 노드
- 내부 노드(비단말 노드) `interal node`  
  : 단말 노드를 제외한 모든 노드  

  > 노드간에는 부모(parent node), 자식(child node), 형제(sibling node)의 상대적인 관계가 성립힌다. (조상, 후손 관계라고 하기도 함)

### 서브 트리(Sub Tree)
큰 트리에 속하는 작은 트리  


<img src="https://user-images.githubusercontent.com/31379392/144812911-35e2fd05-1649-4857-850b-d55de93fc2ca.jpg">
<div>   윤성우 저, 열혈 자료 구조</div>

---
## 08 - 2. 이진 트리 (Binary Tree)
> - 루트 노드를 중심으로 두개의 서브 트리로 나뉘어짐    
> - 나뉘어진 두 서브 트리도 모두 이진 트리이어야 함 => 재귀적인 특성을 지님  
> - 공집합 노드도 이진 트리의 판단에 있어서 노드로 인정  


- 레벨 `level`  
  : 트리의 각 층별로 매긴 숫자. 루트 노드부터 0 레벨로 시작
- 높이 `height`  
  : 트리의 최고 레벨

### 👩‍🏫 포화 이진 트리와 완전 이진 트리
- **포화 이진 트리**  
모든 레벨이 꽉 차서 새로운 노드를 추가하려면 레벨을 늘려야하는 트리
- **완전 이진 트리**   
포화 이진 트리처럼 모든 레벨이 꽉 찬 상태는 아니지만, **차곡차곡 빈 틈 없이 노드가 채워진** 이진 트리    
( 노드가 **위->아래** / **왼쪽->오른쪽**의 순서대로 채워진 것 )  

---
### 👩‍🏫 이진 트리 구현
`배열 기반`  
    : 트리 완성 후, 탐색이 빈번하게 이뤄지는 경우  

`연결 리스트 기반`  
    : 트리를 표현하기에 더 유연하므로 트리 구현시 주로 사용

➡️ 이진 트리에서는 배열 기반 구현도 가능하나 특별한 경우가 아니라면 연결 리스트 기반으로 구현!  

**how to : 연결리스트 기반 구현**  
>1. 필요한 노드 생성 및 초기화
>2. 부모-자식 관계에 맞게 간선 연결

<p align=center><img src="https://user-images.githubusercontent.com/31379392/144811114-06d43356-3a17-4e89-bc7d-66c441955d89.jpg" width = "600"><br>윤성우 저, 열혈 자료 구조</p>

<br></br>

**이진 트리의 노드를 표현한 구조체**
```c
typedef struct _bTreeNode
{
  BTData data;
  struct _bTreeNode * left;   // 왼쪽 자식 노드
  struct _bTreeNode * right;  // 오른쪽 자식 노드
} BTreeNode;
```
💡 자식 노드가 하나도 없는 노드도 그 자체로 이진 트리이므로 트리를 표현한 구조체는 정의하지 않음! ( 공집합 노드가 존재한다고 여김 )  

---
## 08 - 3. 이진 트리의 순회 (Traversal)

### 👩‍🏫 루트 노드를 언제 방문하느냐
<p align=center><img src="https://user-images.githubusercontent.com/31379392/145024213-b5a4e966-378a-430b-8355-eb73845af0db.jpg" width = "600"><br>윤성우 저, 열혈 자료 구조</p>  

1. 먼저 ➡️ **전위 순회** `Preorder Traversal`
2. 중간에 ➡️ **중위 순회** `Inorder Traversal`
3. 마지막에 ➡️ **후위 순회** `Postorder Traversal`

💡 높이가 2 이상인 이진 트리는 어떻게 순회하나? ➡️ [재귀적으로 구현](#👩‍🏫-순회의-재귀적-표현-:-중위-순회)
### 👩‍🏫 순회의 재귀적 표현 : 중위 순회
<p align=center><img src="https://user-images.githubusercontent.com/31379392/145025601-54d04ebb-5047-4f0c-a661-f7454e3ada83.jpg" width = "300"><br>윤성우 저, 열혈 자료 구조</p>  

**how to**
> 1. 왼쪽 서브 트리의 순회  
> 2. 루트 노드의 방문  
> 3. 오른쪽 서브 트리의 순회  
>   
> * 각 서브 트리에서의 순회에서도 동일한 방법으로 실행

```c
void InorderTraverse(BTreeNode * bt, VisitFuncPtr action)
{
  if(bt == NULL)                        // 재귀 탈출조건
    return;

  InorderTraverse(bt->left, action);   // 1. 왼쪽 서브 트리
  action(bt->data);                    // 2. 노드 방문시 수행할 액션 & 루트 노드 방문
  InorderTraverse(bt->right, action);  // 3. 오른쪽 서브 트리
}
```
💡 전위 순회와 후위 순회 방식은 방문하는 순서만 변경하면 됨


---
## 08 - 4. 수식 트리(Expression Tree)의 구현
이진 트리를 이용하여 **수식을 표현**해 놓은 것. 이진 트리와 별개의 것이 아님!


- 연산자 : 루트 노드
- 피연산자 : 2개의 자식 노드  

<p align=center><img src="https://user-images.githubusercontent.com/31379392/145036990-63ec75f0-acf6-4ce3-b964-5d4122b88e66.jpg" width = "600"><br>윤성우 저, 열혈 자료 구조</p>

**how to**  
> 중위 표기법의 수식 ➡️ 후위 표기법의 수식 ➡️ 수식 트리  
>   
> * 중위 표기법 -> 후위 표기법 : Ch 06에서 정의  
>  
> **후위 표기법의 수식을 수식 트리로 바꾸는 일에 집중!**


### 👩‍🏫 수식 트리 구성 : 후위 표기법의 수식 기반
트리의 **하단부터 시작**해서 점진적으로 트리의 윗부분을 구성  

**how to**  
피연산자를 만나면 **스택**에 넣고, 연산자를 만나면 **스택**에서 꺼낸다!  
> 1. 피연산자 등장 ➡️ 스택에 넣음  
> 2. 연산자가 등장 ➡️ 스택에 쌓인 피연산자(or 서브 트리)를 모두 꺼내 `연산자는 부모 노드 - 피연산자(or 서브 트리)는 자식 노드`로 연결, 서브 트리 구성  
> 3. 만들어진 서브 트리는 다시 스택에 넣음 (서브 트리의 루트 노드 주소를 넣으면 됨)
> 4. 수식이 끝날 때까지 반복

### 👩 수식 트리의 계산
**how to**
> 1. 자식 노드에 저장된 피연산자 확인  
>    ➡️ 자식 노드가 서브 트리일 경우를 고려해서 재귀함수 사용  
> 2. 부모 노드에 저장된 연산자 확인  
> 3. 계산  
```c
int EvaluateExpTree(BTreeNode * bt)
{
  int op1, op2;

  // 재귀 탈출 조건 - 자식 노드가 서브 트리가 아닌 단말 노드라면
  if(GetLeftSubTree(bt)==NULL && GetRightSubTree(bt)==NULL)
    return GetData(bt);

  // 1. 피연산자 - 자식노드가 단말노드가 아닌 서브 트리일 경우를 고려해서 재귀함수 사용
  op1 = EvaluateExpTree(GetLeftSubTree(bt));
  op2 = EvaluateExpTree(GetRightSubTree(bt));

  // 2. 연산자 확인
  switch(GetData(bt))
  {
    // 3. 연산자에 따른 연산 수행
  }
  return 0;
}
```
---
