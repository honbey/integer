# Integer

Big integer operation.

C 语言实现的大整数运算，包含了加、减、乘、除、模、移位这几种基本运算。理论上最大支持的整数为 $(2^32)^{2^31}$。


## 起源

大三的密码学用 C++ 实现了 $2^63$ 内的 RSA 算法，当时也在积极探索大整数的实现方式，实现了一版[bigint](https://git.freewisdom.cn/honbey/learn-corcpp/src/branch/master/bigint/bigint.c)，不过模幂运算有点问题，后来由于期末考试就搁置了，后面大四开始实习等等，一直没弄。毕业的六月等证的时期倍感无聊，开始整理大学中的写的代码，整理到密码学的代码时觉得很有必要好好实现下大整数。


## 实现

加减乘算法主要是基于手工运算的步骤，整除的实现有点特殊。


## 测试

代码没有经过严格的测试，当前只是使用随机生成的大整数配合 python 进行的测试。


## 更新日志

### 20210615

- 为方便运算，新增了两个基本运算的接口
- 素性测试采用 Miller - Rabin 方法，实现代码较为复杂，代码暂未提交
- 增加了大整数与 `uint32_t` 类型的四则基本算术运算接口
- 完成了一个字符串形式的十进制大整数转 Integer 的函数
- 一个简单 RSA 算法测试，所用的大素数由命令 `openssl prime -generate -bits 960` 生成

### 20210614

- 加减法还原了对循环的优化以解决某些错误运算问题
- 完成模幂运算，使用随机数进行了测试得到正确结果
- 完成求模逆的函数，对加减法的逻辑判断进行了优化
- 利用欧几里得算法求最大公约数
- 修复了除法中存在的小数减大数的问题

### 20210613

- 增删了一些文件，改变了头文件的结构，减少了不必要的 include
- 使用 inline 内联函数提升部分函数的效率，同时隐藏了一些用于内部实现的函数
- 对四则基本运算函数的代码进行了优化，减少不必要的函数调用和循环次数
> 优化后，四则基本的算术运算需要通过特定函数调用，特定函数实现了对特殊情况的处理，同时保证了正确传递函数参数，实际的算术运算函数不允许除特定函数外的函数进行调用，因为使用不当的话后果未知

### 20210612

完成整数的表示以及四则基本运算，使用少量随机数进行了测试。


## 待办

- [x] 大整数的表示
- [x] 加、减、乘、除
- [x] 模运算
- [x] 模幂运算
- [ ] 素性测试
- [ ] 大整数的 RSA 算法
- [ ] 完善测试
