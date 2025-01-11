## 数组 | vector

- 初始化：
```cpp
vector<int> vec; // 创建一个空的int类型vector
vector<int> vec(5); // 创建一个包含5个元素的vector，每个元素初始化为0
vector<int> vec(5, 10); // 创建一个包含5个元素的vector，每个元素初始化为10
vector<int> vec = {1, 2, 3, 4, 5}; // 使用列表初始化

//矩阵初始化
int a = 3; // 行数
int b = 4; // 列数
vector<vector<int>> matrix(a, vector<int>(b, 0)); // 初始化为a行b列，所有元素为0
```

- 增删元素：
```cpp
vec.push_back(6); // 在vector末尾添加一个元素
vec.pop_back(); // 删除最后一个元素
vec.erase(vec.begin() + 2); // 删除第三个元素
vec.erase(vec.begin(), vec.begin() + 2); // 删除从第一个元素到第二个元素（不包括）
```

- 访问元素：
```cpp
int first = vec[0]; // 访问第一个元素
int last = vec.back(); // 访问最后一个元素
int at = vec.at(2); // 安全访问第三个元素，如果越界会抛出std::out_of_range异常
```

- 插入元素：
```cpp
vec.insert(vec.begin() + 2, 10); // 在第三个位置向前插入元素10
vec.insert(vec.begin() + 2, 3, 10); // 在第三个位置向前插入3个元素，每个都是10
vector<int> moreElements = {7, 8, 9};
vec.insert(vec.begin() + 2, moreElements.begin(), moreElements.end()); // 在第三个位置插入另一个vector的元素
```

- 容量检测：
```cpp
vec.size(); //获取vector中元素数量
vec.empty(); //检查vector是否为空   
```

- 交换和清空：
```cpp
std::vector<int> anotherVec = {10, 11, 12};
vec.swap(anotherVec); // 交换两个vector的内容
vec.clear(); // 移除所有元素，vector变为空   
```

- 排序和搜索：
```cpp
std::sort(vec.begin(), vec.end()); // 使用默认比较器升序排序vector
auto it = std::find(vec.begin(), vec.end(), 10); // 搜索第一个值为10的元素的迭代器
```

---

## 表 | list

本质上是一个双向队列，内存上存放不连续，因此**不能通过索引来访问**，只能够通过迭代器来访问，语法类似于指针： `*it` 返回 `it` 对应表中的数据元素

- 初始化声名：
```cpp
list<int> mylist;
```

- 添加元素：
```cpp
mylist.push_back(10); //末尾追加元素10
mylist.push_front(5); //开头追加元素5

list<int>::iterator it = mylist.begin(); //最为标准的写法
auto it = mylist.begin(); //直接auto也是一样的
++it; // 移动到第二个元素
mylist.insert(it, 30); // 在原索引1处向前插入30
```

- 通过迭代器遍历：
```cpp
for(auto it = mylist.begin(); it != mylist.end(); it++){
	cout<< *it <<" "; // *it 返回对应值
}
```

- 删除：
```cpp
mylist.pop_back(); //末尾弹出
mylist.pop_front(); //先头弹出

auto it = myList.begin();
++it; // 移动到第二个元素
mylist.erase(it); // 删除第二个元素

mylist.clear(); //清空
```

---

## 二元组 | pair

C++中内置的专门用于存放数据对的数据类型

- 初始化声名：
```cpp
// 直接使用模板参数
pair<int, string> p1(1, "Kimi");

// 使用 make_pair
pair<int, string> p2 = make_pair(1, "Kimi");

//初始化列表
pair<int, string> p3 = {1, "Kimi"};
```

- 访问成员：
```cpp
pair<int, string> p = {1, "Kimi"};
int a = p.first;    // a 的值是 1
string b = p.second; // b 的值是 "Kimi"
```

> [!NOTE] 注意
> unordered_set 默认不支持 pair 类型，因为其中的哈希相等未定义

---

## 栈 | stack

stack可以使用vector来实现

```cpp
stack<int> myStack;
int a=0;
myStack.push(a); //压栈
int top_element = myStack.top(); //访问栈顶
myStack.pop(); //弹出
bool empty = myStack.empty(); //返回栈是否为空
```

---

## 队列 | queue

包含在头文件 `<queue>` 中

- 初始化：
```cpp
queue<int> q; //初始化队列
```

- 增减元素：
```cpp
q.push(10); //加入一个元素10
q.pop(); //从队首弹出元素
```

- 访问元素：
```cpp
int frontValue = q.front(); // 获取队首元素
int backValue = q.back(); // 获取队尾元素
```
---

## 堆 | heap

### 一般操作
在C++中叫“优先队列”，和堆是一个东西；包含在 `<queue>` 中，关键词为：`priority_queue`

- 初始化：
```cpp
//不写后面两个参数默认为vector，less
priority_queue<int> pq1;
//建立一个优先级队列(大堆)，数据类型是int，利用vector容器实现，less(大根堆)
priority_queue<int, vector<int>, less<int>> pq2;
//建立一个优先级队列(小堆)，数据类型是int，利用vector容器实现，greater(小根堆)
priority_queue<int, vector<int>, greater<int>> pq3;
```

- 常见操作：
```cpp
pq.top(); //返回第一个元素的引用
pq.push(); //插入一个元素并维护堆，无返回值
pq.pop(); //删除优先级最高的元素，无返回值
pq.size(); //返回队列元素数目
```

![[标准函数#堆操作]]

### 对 pair 类型建堆
对于 `pair` 类型的数据，需要自己定义一个**比较类**才能够进行建堆操作；

```cpp
//定义比较类
class cmp{
	public:
	bool operator()(pair<int,int> &a, pair<int,int> &b){
		return a.first > b.first; //基于第一个值进行排序
	}
};

//堆声名
priority_queue<pair<int,int>, vector<pair<int,int>>, cmp> pq;
```

---

## 哈希表 | hash

C++中叫无序映射表，用于存储键值对，包含在 `<unordered_map>` 中
- 声名和初始化：
```cpp
unordered_map<int, int> hmap; // 声名

unordered_map<int, int> hmap{ {1,10},{2,12},{3,13} };

//如果知道要创建的哈希表的元素个数时，也可以在初始化列表中指定元素个数
unordered_map<int, int> hmap{ {{1,10},{2,12},{3,13}},3 };
```

- 插入元素：
```cpp
// 通过下标运算插入元素
hmap[5] = 15;

//通过insert函数进行插入
hmap.insert({5, 15});
```

> [!NOTE] 注意
> 使用下标运算进行插入时，对同一个键重复插入会产生覆盖；而使用 insert 插入时，重复插入会无效，值依然是第一次创建时的值

- 删除元素：
```cpp
unordered_map<int, int> hmap{ {1,10},{2,12},{3,13} };
unordered_map<int, int>::iterator iter_begin = hmap.begin();
unordered_map<int, int>::iterator iter_end = hmap.end();

hmap.erase(iter_begin);  //删除开始位置的元素
hmap.erase(iter_begin, iter_end); //删除开始位置和结束位置之间的元素
hmap.erase(3); //删除key==3的键值对
hmap.clear(); //清空哈希表
```

- 元素统计：
```cpp
int count = hmap.count(key);
//因为unordered_map不允许重复元素，所以返回值为0或1
```

- 妙用：将值映射为一个数组，可以实现**一对多**的映射关系
```cpp
unordered_map<string, vector<string>> mp;
for (string& str: strs) {
	string key = str;
	sort(key.begin(), key.end()); //对key重排，可能产生重复
	mp[key].emplace_back(str); // 用vector存储key相同的字符串
}
```

---

## 无序集合 | set

如果只需要考虑去除重复的 key 值的话，可以考虑使用更加简便的 `unordered_set`，相当于一个没有对应值的哈希表

- 初始化：
```cpp
unordered_set<int> uset;
unordered_set<int> uset = {10, 20, 30}; //带有初始值的声名
```

- 加入 key 值：
```cpp
uset.emplace(5) //加入键值5
uset.insert(15) //直接使用insert函数插入元素15
```

- 统计：
```cpp
int isFound = uset.count(5) //查询 key 值5的出现次数，只有0/1两个取值
```

- 删除操作：
```cpp
uset.erase(5); //在uset中删除键值为5的元素

//传入迭代器，会删除迭代器指向的元素
auto it = uset.begin() + 2;
uset.erase(it); //删除索引为2的元素
```

---
