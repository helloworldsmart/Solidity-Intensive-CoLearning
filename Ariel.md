---
timezone: Asia/Shanghai
---

# YourName

1. 自我介绍
我是Ariel,在參與本次共學前從未接觸過Solidity 與智能合約相關知識，發現自己太多不了解的知識，想要扎實從頭學起～

2. 你认为你会完成本次残酷学习吗？
我覺得我可以完成本次殘酷共學。為了完成此次學習，我有空出每天一段時間，希望可以幫助我成功完成學習。
   
## Notes

<!-- Content_START -->

### 2024.09.23

學習內容: 
WTF Academy #1-5
![1000005316](https://github.com/user-attachments/assets/8a67b9f8-ff71-43a5-bf23-3eefc2545d19)

# 2: enum枚举:uint 分配名稱與維護

# 3: 函數類型：prue/view

# 4: 函數輸出：命名式返回/結構式賦值（读取函数的全部或部分返回值）

# 5: 儲存位置
1.
store:狀態變量、上鏈
memory：參數與臨時變量，內存中不上鏈
calldata：類memory,不可修改

2. 會影響變量：
storage->storage
memory ->memory

3. 作用域：

狀態：鏈上，gas消耗高
局部：函數執行過程中，內存，完成消失，函數內聲明
全局：可不聲明，為預留關鍵字

3个常用的全局变量：msg.sender，block.number和msg.data，他们分别代表请求发起地址，当前区块高度，和请求数据。下面是一些常用的全局变量，更完整的列表请看这个链接：
blockhash(uint blockNumber): (bytes32) 给定区块的哈希值 – 只适用于256最近区块, 不包含当前区块。
block.coinbase: (address payable) 当前区块矿工的地址
block.gaslimit: (uint) 当前区块的gaslimit
block.number: (uint) 当前区块的number
block.timestamp: (uint) 当前区块的时间戳，为unix纪元以来的秒
gasleft(): (uint256) 剩余 gas
msg.data: (bytes calldata) 完整call data
msg.sender: (address payable) 消息发送者 (当前 caller)
msg.sig: (bytes4) calldata的前四个字节 (function identifier)
msg.value: (uint) 当前交易发送的 wei 值
block.blobbasefee: (uint) 当前区块的blob基础费用。这是Cancun升级新增的全局变量。
blobhash(uint index): (bytes32) 返回跟当前交易关联的第 index 个blob的版本化哈希（第一个字节为版本号，当前为0x01，后面接KZG承诺的SHA256哈希的最后31个字节）。若当前交易不包含blob，则返回空字节。这是Cancun升级新增的全局变量。


4. 乙太單位
精度表示，以0代替小數點
wei: 1
gwei: 1e9 = 1000000000
ether: 1e18 = 1000000000000000000

5. 時間單位

### 2024.09.24
學習內容：WTF #6~8
![image](https://github.com/user-attachments/assets/00a41a16-a6e3-4284-a1e8-7a2c5d1aed52)

# 6:引用類型
   1. array:
      1. 固定(內存）：uint[8] array1;
      3. 可變(動態) ：uint[] array1;
      4. 例外：
         1. bytes array7; 不用加［］，叫省gas
         2. bytes1[] array5; 要加
      5. 數組創建：
         1. memory修饰的动态数组，可以用new操作符来创建，但是必须声明长度，并且声明后长度不能改变
            uint[] memory array8 = new uint[](5);
         2. 一个值没有指定type的话，会根据上下文推断出元素的类型，默认就是最小单位的type
             g([uint(1), 2, 3]); -->都是uint
         3. 數組成員
               1. memory內存數組:length
               3. 動態數組:push()最後添加0/push(x)最後添加x/pop()移除最後元素
   2. struct:定義新類型,可為原始/引用；本身可作為數組or mapping元素 ，struct中不可包含其本身。可含數組/mapping/struct類型
      1. 四種賦予值方法
         1.Student storage _student = student; // assign a copy of student
            _student.id=1;
         2. 直接引用状态变量的struct
           student.id=1;
         3. 構造函數式：student = Student(3, 90);
         4. key value:student = Student({id: 4, score: 60});

# 7: 映射類型：存key value pair table, hash table
   1. 格式：mapping(_KeyType => _ValueType)
         例：mapping(uint => address) public idToAddress; // id映射到地址
            mapping(address => uint) public balance0f; //记录不同地址的持仓数量
   3. 注意：
      1. _KeyType只能選預設類型，無法用自定義結構體，_ValueType則可
      2. 存储位置必须是storage，可用於合約狀態變量
      3. 如果映射声明为public，那么Solidity会自动给你创建一个getter函数，可以通过Key来查询对应的Value
      4. 新增鍵值對：
         function writeMap (uint _Key, address _Value) public
         {
             idToAddress[_Key] = _Value;
         }
   4. 原理：
      1. 不存key資訊，無length資訊
      2. 使用keccak256(abi.encodePacked(key, slot))作為offset存取value，slot是映射變量定義所在插槽
      3. 定义所有未使用的空间为0，初始值為默認值

# 8：變量初始值
      1. 值/引用 類型
         1. 值：
            boolean: false
            string: ""
            int: 0
            uint: 0
            enum: 枚举中的第一个元素
            address: 0x0000000000000000000000000000000000000000 (或 address(0))
            function
            internal: 空白函数
            external: 空白函数

         2. 引用
            映射mapping: 所有元素都为其默认值的mapping(即a=>b中b的默認值)
            结构体struct: 所有成员设为其默认值的结构体
            数组array
               动态数组: []
               静态数组（定长）: 所有成员设为其默认值的静态数组
               eg:byte1初始值為0x00

      2. delete操作符
         dalete a; //變量a還原初始值

### 2024.09.25

學習內容：WTF #9-11

![image](https://github.com/user-attachments/assets/57aecb5b-19c1-43d9-b848-4ebfd3c5e4f8)


# 9:常數
   1. constant
      1. 数值变量可以声明constant和immutable
      2. string和bytes可以声明为constant，但不能为immutable
      3.初始化之后，尝试改变它的值，会编译不通过
      4. 必須聲明時初始化，後不可變
         ~ uint256 constant CONSTANT_NUM = 10;
   2. immutable
      1. 靈活，可在聲明或構造函數時初始化
      2. Solidity v8.0.21以后，immutable变量不需要显式初始化。反之，则需要显式初始化。
      3.初始化之后，尝试改变它的值，会编译不通过
      4. immutable變量同時在聲明和constructor中初始化-->使用constructor初始化值
         ```
         constructor()
         {
            IMMUTABLE_ADDRESS = address(this);
            IMMUTABLE_NUM = 1118;
            IMMUTABLE_TEST = test();
         }
         ```

# 10:控制流
   https://www.wtf.academy/docs/solidity-101/InsertionSort
   1. if-else
   2. for
   3. while
   4. do-while
   5. 三元運算符：条件? 条件为真的表达式:条件为假的表达式
   6. continue/break
   7. 插入排序
```
               // 插入排序 正确版
         function insertionSort(uint[] memory a) public pure returns(uint[] memory) {
             // note that uint can not take negative value
             for (uint i = 1;i < a.length;i++){
                 uint temp = a[i];
                 uint j=i;
                 while( (j >= 1) && (temp < a[j-1])){
                     a[j] = a[j-1];
                     j--;
                 }
                 a[j] = temp;
             }
             return(a);
         }
```
notice: 
   - line178: uint j=i;
   - line179-180: uint j >= 1   &   a[j] = a[j-1];


# 11:構造函數和修飾器
   1. constructor
         1. 每个合约可以定义一个，在部署合约的时候自动运行一次
         2. 可以用来初始化合约的一些参数，如owner地址
            ```
            constructor(address initialOwner)
            {
                owner = initialOwner; // 在部署合约的时候，将owner设置为传入的initialOwner地址
            //舊寫法 Parents
            }
            ```
   2. modifier：运行函数前的检查，例如地址，变量，余额
      ```
         modifier onlyOwner
          {
               require(msg.sender == owner); // 检查调用者是否为owner地址
               _; // 如果是的话，继续运行函数主体；否则报错并revert交易
               //onlyOwner修饰符的函数只能被owner地址调用
          }

         function changeOwner(address _newOwner) external onlyOwner
               {
                  owner = _newOwner; // 只有owner地址运行这个函数，并改变owner
               }
      ```
OpenZeppelin是一个维护Solidity标准化代码库的组织，他的Ownable标准实现如下： https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/access/Ownable.sol


### 2024.09.

學習內容：WTF #12-

# 12:事件











<!-- Content_END -->
