

# YourName

1. 自我介绍

2. 你认为你会完成本次残酷学习吗？
   
## Notes

<!-- Content_START -->

### 2024.09.23

今天學了function, event, static variables, 還有好像是qualifier一樣的東西，constant, internal, private, public。 
function還有modifier，可以設置啟動某function的條件。
還學到了boollean和一些運算式，很多都是比以前學過的東西。
現在就算小小複習一下，明天會更認真學！

### 2024.09.24

**constant**
constant变量必须在声明的时候初始化，之后再也不能改变。尝试改变的话，编译不通过。
**immutable**
immutable变量可以在声明时或构造函数中初始化，因此更加灵活。在Solidity v8.0.21以后，immutable变量不需要显式初始化，未显式初始化的immutable变量将使用数值类型的初始值（见 8. 变量初始值）。反之，则需要显式初始化。 若immutable变量既在声明时初始化，又在constructor中初始化，会使用constructor初始化的值。

### 2024.09.25
今天試著做一個很簡單的計算器還有一個很簡單的Twitter工具，然後deploy，view on etherscan.
另外還去了Ethereum Sepolia Faucet 拿了一點testnet用的Eth。

```
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.0;
contract Calculator {
    uint256 result = 0;
    function add( uint256 num) external {
        result += num;
    }
    function subtract(uint256 num) public {
        result -= num;
    }
    function multiply(uint256 num) public {
        result *= num;
    }
    function get() public view  returns (uint256) {
        return result;
    }
}
```
另外學了Mapping和array。
Mapping，就相當於給每個value 一個 key
每個Array都有對應的從0開始的Index. 
以上。






<!-- Content_END -->
