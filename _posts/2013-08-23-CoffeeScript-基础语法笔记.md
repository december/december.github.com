---
layout: post
category: JavaScript
tags: CoffeeScript JavaScript
description: CoffeeScript 可以避免 Java 形式的代码的重复和冗余，让你像写 Ruby 代码一样精简而优美的写 Javascript
---

### 本地执行环境搭建

   1. 安装 nodejs

        sudo add-apt-repository ppa:chris-lea/node.js
        sudo apt-get update
        sudo apt-get install nodejs

  2. 安装 CoffeeScript

        sudo npm install coffee-script


### 变量定义

  1. 创建变量, CoffeeScript 在变量赋值前，自动为变量添加 var

        for = 'far'

  2. 创建全局变量（在顶级作用越中，this 相当与全局对象）

        global = this
        global.for = bar    # 执行这两句代码后，就全局变量 for 等于 bar 了

### 函数定义

  1. 用 `->` 定义一个 function，并自动把在函数最后一行加上 return

        func = ->
          'return value'

  2. 函数参数

        func = (x, y) ->
        func = (x = 1, y = 2) ->
        func = (x, y...) ->        # y 是一个数组

  3. 使用 `=>` 定义函数，来绑定函数定义时的上下文环境到函数中

        func = (x) =>
          
### 流程控制

  1. if 表达式
  
        # CoffeeScript 不支持三目运算符，可以这样替代
        if 1 > 0 then 'yes' else 'no'

  2. 说明：可以使用 not 来替代感叹号（！）, 使用 is 编译过后就是 ===， 使用 isnt 来代替 is not 以增加可读性；CoffeeScript 会自动把 == 操作符转化为 ===，把 != 转化为 !==

### 字符串插值
CoffeeScript 支持 Ruby 风格的字符串插值方式

    name = 'tom'
    user = "name: #{name}"

### 循环和列表解析
循环返回一个由循环最后一行的值组成的数组

  1. 使用 for x in array
  
        for name in ['tom', 'jack', 'marry']
          alert name
        # 上面方式可以简写成：
        alert name for name in ['tom', 'jack', 'marry']

  2. 循环加入索引

        alert "#{name} - #{i}" for name, i in ['tom', 'jack', 'marry']
        
  3. 数组循环的过滤

        alert "#{name} - #{i}" for name, i in ['tom', 'jack', 'marry'] when i < 2

  4. 使用 of 替代 in 关键字来迭代对象的全部属性，像 Ruby 中的 hash 迭代一样

        names =
          tom: 'man'
          marry: 'woman'

        for name, sex of names
          alert "#{name} - #{sex}"

  5. 也可以使用 CoffeeScript 唯一暴露的顶层循环 while

### 数组

  1. 受 Ruby 影响，CoffeeScript 可以使用两个数组来定义区间

        range = [1..3]   # range = [1,2,3]

  2. 分割一个数组（如果一个区间被指定到一个数组之后，CoffeeScript 会将其转换为一个 slice() 调用）

        variable = ["one", "two", "three"][0..1]    # variable = ["one", "two"]

  3. 替换数组片段的值

        numbers = [1..4]
        numbers[1..2] = [-1, -2]    # numbers = [1, -1, -2, 4]

  4. 在字符串上也可以使用区间来获得一个新的子字符串

        str = 'test'[0..1]    # str = 'te'

  5. 检测数组是否存在某个值，使用 `in` 操作符

        strs = ['a', 'b', 'c']
        console.log 'a' if 'a' in strs

### 存在检查
CoffeeScript 存在操作符 `?` 只会在变量不为 `null` 或者 `undefined` 的时候会返回 `true`，与 Ruby 的 nil? 类似

    true if name?

还可以使用 `?` 来替代 `||` 操作符

    default = name ? 'tom'    # 'tom'

如果要在访问属性，函数之前进行 `null` 检查，我们可以吧 `?` 放在调用的属性方法的左边来跳过编译时的语法检查，这与 Rails 的 try 方法相似

    
