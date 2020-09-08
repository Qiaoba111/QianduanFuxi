### vue学习

#### 一、防抖函数

- 对于refresh非常频繁的问题，进行防抖操作

  - 防抖debounce/节流throttle
  - 防抖函数起作用的过程
    - 如果我们直接执行refresh,那么refresh韩硕会被执行30次
    - 可以将refresh函数传入到debounce函数中，生成一个新的函数
    - 之后在调用非常频繁的时候，就使用新生成的函数
    - settimeout下一次循环的时候执行

  ```     javascript
     debounce(func,delay){
        let timer = null
        return function(...args){
          if(timer) clearTimeout(timer)
          timer = setTimeout(()=>{
            func.apply(this,args)
          },delay)
        }
      }
  ```

#### 二、上拉加载更多

#### 三、tabControl的吸顶效果

##### 3.1 获取到tabControl 的offsetTop

- 必须知道滚到多少时，开始有吸顶效果，这个时候就需要获取tabControl的offsetTop
- 但是如果直接在mounted中获取tabControl的offsetTop，那么值是不正确的
- 如何获取正确的值？
  - 监听HomSwiper中的img的加载完成
  - 加载完成后，发出事件，在Home.vue中，获取正确的值。
  - 补充
    - 为了不让HomeSwiper多次发出事件
    - 可以使用isLoad的变量进行状态的记录
  - 注意这里不进行多次调用和debonce的区别

##### 3.2、监听滚动，动态改变tabControl的样式

- 问题：动态的改变tabControl的样式时，会出现俩个问题：

  - 问题一：下面的商品内容，会突然上移
  - 问题二：tabControl虽然设置了fixed，但是也随着Better-Scroll一起滚出去了

- 其他方案来解决停留问题

  - 在最上面，多复制了一份TabControl组件对象，利用它来实现停留效果
  - 当用户滚动到一定位置时，PlaceHolderTabControl显示出来
  - 当用户滚动没有达到一定位置时PlaceHolderTabControl隐藏起来

  





​       