---
layout:     post   				    # 使用的布局（不需要改）
title:      自动化测试：Selenium WebDriver完结篇			 
subtitle:   Selenium 完结 #副标题
date:       2025-11-16				# 时间
author:     wuxia						# 作者
header-img: img/post-bg-2015.jpg	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签

  - spider
  - Selenium
---

## [自动化测试](https://so.csdn.net/so/search?q=%E8%87%AA%E5%8A%A8%E5%8C%96%E6%B5%8B%E8%AF%95&spm=1001.2101.3001.7020)——selenium（完结篇)

#### 文章目录

  * 自动化测试——selenium（完结篇)
    * 一、元素操作方法
    * 二、浏览器操作方法
    * 三、获取元素信息操作
    * 四、鼠标操作 （需要实例化鼠标对象）
      * 4.1 鼠标右键及双击
      * 4.2 鼠标拖拽
      * 4.3 鼠标悬停 【重点】
    * 五、键盘操作（不需要实例化对象）☆
    * 六、元素等待
    * 七、下拉框（需要实例化下拉框）
    * 八、弹出框
    * 九、滚动条
    * 十、切换frame表单 ☆
        * 10.1 连续切换frame
    * 十一、多窗口的切换 ☆
    * 十二、截图操作
    * 十三、验证码

>
> 前言：看这篇帖子，最好要在知道定位八大元素的基础之上才能够比较熟练的看完这篇帖子，[selenium八大元素基础](https://blog.csdn.net/qq_54219272/article/details/123310772?spm=1001.2014.3001.5501)
> ，点击这个链接，这个链接是八大元素定位的帖子。

### 一、元素操作方法

```
方法：
1、.send_keys()  # 输入方法
2、.click()  # 点击方法
3、.clear()  # 清空方法
```



> 注意：在输入方法之前一定要清空操作!!

```
# 导包

from time import sleep
from selenium import webdriver

# 实例化浏览器

driver = webdriver.Chrome()

# 打开网址

driver.get('https://www.baidu.com/')

# 需求

ele = driver.find_element_by_css_selector('#kw')
ele.send_keys('易烊千玺')
sleep(2)

# 清空

ele.clear()
ele.send_keys('王嘉尔')

# 时间轴看效果

sleep(3)

# 关闭页面

driver.quit()
```

![浏览器清除](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/385806db6ba0f3e7c028b50300b0085b.gif)

### 二、浏览器操作方法

常用的浏览器操作系统API

```
# 方法

"""
1、driver.maximize_window()  # 最大化浏览器
2、driver.set_window_size(w,h)  # 设置浏览器大小 单位像素 【了解】
3、driver.set_window_position(x,y)  # 设置浏览器位置  【了解】
4、driver.back() # 后退操作
5、driver.forward() # 前进操作
6、driver.refrensh() # 刷新操作
7、driver.close() # 关闭当前主窗口（主窗口：默认启动那个界面，就是主窗口）
8、driver.quit() # 关闭driver对象启动的全部页面
9、driver.title # 获取当前页面title信息
10、driver.current_url # 获取当前页面url信息
"""
```

```
"""
应用：driver.maximize_windows()  # 窗口最大化
    driver.set_window_size(w,h) # 设置浏览器大小 【了解】
    driver.set_window_position(x,y) # 设置浏览器窗口位置 【了解】
"""

from time import sleep
from selenium import webdriver

driver = webdriver.Chrome()

driver.get('https://www.baidu.com/')

# 窗口最大化

driver.maximize_window()
sleep(1)

# 设置浏览器宽，高 【了解】

driver.set_window_size(1000, 1000)
sleep(1)

# 设置窗口浏览器位置  【了解】

driver.set_window_position(200, 200)

sleep(3)

driver.quit()
```

![浏览器位置切换](https://i-blog.csdnimg.cn/blog_migrate/81ccb9e8ed2a83ba1570d74654d322e6.gif)

```
"""
driver.back()
driver.forward()
driver.refresh()
"""
from time import sleep
from selenium import webdriver

driver = webdriver.Chrome()

driver.get('https://www.sogou.com/')
driver.find_element_by_css_selector('#query').send_keys('易烊千玺')
driver.find_element_by_id('stb').click()
sleep(2)

# 后退

driver.back()
sleep(2)

# 前进

driver.forward()
sleep(2)

# 刷新

driver.refresh()

sleep(3)

driver.quit()
```

![请添加图片描述](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/a7fb848803ae0976e4855929f05c9909.gif)

```
"""
driver.close() # 关闭当前主窗口，默认启动的界面就是主窗口
driver.quit() # 关闭全部页面
driver.title  # 获取页面标题
driver.current_url  # 获取页面地址 
"""

from time import sleep
from selenium import webdriver

driver = webdriver.Chrome()

driver.get('https://www.sogou.com/')
driver.find_element_by_link_text('图片').click()

# 这两个属性可以用来做断言使用

print("当前页面标题：", driver.title)
print("当前页面的url：", driver.current_url)

# 这里关闭的是原始页面，而不是新的页面，只有完成页面切换才可以关闭新的页面

# 场景：关闭单个页面使用

driver.close()
sleep(3)

# 关闭浏览器驱动对象的所有页面

driver.quit()
```

注意：`driver.close()` ，当前关闭的是主窗口，只有完成页面切换才可以关闭当前新的页面

提示：

1、`driver.title` 和 `drivet.current_url`是属性没有括号。应用场景：一般判断上不操作是否执行成功。

2、`driver.maximize_window()` 一般为前置代码放到获取driver地址后，进行浏览器窗口的最大化

3、`driver.refresh()` 向浏览器重新发出请求，刷新页面，在cookie 会用到

4、`driver.close()` 和 `driver.quit()` 的区别：

  * `close()`:关闭当前主窗口
  * `quit()`:关闭由driver对象启动的所有页面
  * 如果只有一个窗口那么`quit（）`和 `close（）`没有区别。

### 三、获取元素信息操作

常用元素信息操作API

```
"""
方法：
1、text 获取元素的文本； 如：driver.text
2、size 获取元素的大小： 如：driver.size
3、get_attribute 获取元素属性值；如：driver.get_attribute("id") ,传递的参数是元素的属性名
4、is_displayed 判断元素是否可见 如：element.is_displayed()
5、is_enabled 判断元素是否可用 如：element.is_enabled()
6、is_selected 判断元素是否被选中 如：element.is_selected()

"""
```

```
"""
text  获取元素文本 ,没有（）
size  获取元素大小 ，没有（）
get_attribute("属性名") 获取的是属性值
"""

from time import sleep
from selenium import webdriver

driver = webdriver.Chrome()

driver.get('https://www.sogou.com/')
ele = driver.find_element_by_id('query')
print("目标元素尺寸：", ele.size)

new_ele = driver.find_element_by_id('hanyu')
print("目标元素文本：", new_ele.text)

link = driver.find_element_by_link_text("图片")
print("目标元素属性值：", link.get_attribute('id'))

sleep(3)

# 关闭浏览器驱动对象的所有页面

driver.quit()
```

```
"""
is_displayed() 判断元素是否可见，如：element.is_displayed
is_enabled() 判断元素是否可用， 如：element.is_enabled
is_selected() 判断元素是否被选中，如：element.is_selected
"""

from time import sleep
from selenium import webdriver

driver = webdriver.Chrome()

driver.get('file:///D:/%E6%A1%8C%E9%9D%A2/page/%E6%B3%A8%E5%86%8CA.html')

# 判断元素是否可见，不可见并不代表不能定位

span = driver.find_element_by_name('sp1')
print("元素是否可见：", span.is_displayed())

btn = driver.find_element_by_id('cancelA')
print("元素是否可用：", btn.is_enabled())

check = driver.find_element_by_id('lia')
print("元素是否被选中：", check.is_selected())

sleep(3)

# 关闭浏览器驱动对象的所有页面

driver.quit()
```

注意：里面的返回的结果都是`True` 和 `False`。

### 四、鼠标操作 （需要实例化鼠标对象）

1、我们有了鼠标为什么还要使用鼠标操作？？

 为了满足丰富的html鼠标效果，必须使用对应的方法。

2、鼠标时间对应的方法在那个类中？

 `ActionChains`类,`实例化 鼠标对象`

导包：  

```
from selenium.webdriver.common.action_chains import ActionChains
```

3、鼠标事件常用的操作 ☆

```
"""
1、context_click(element) # 右击
2、double_click(element)  #双击
3、double_and_drop(source, target)  # 拖拽
4、move_to_element(element)  # 悬停 【重点】
5、perform()  # 执行以上事件的方法 【重点】
"""
```



#### 4.1 鼠标右键及双击

```
"""
鼠标操作：
context_click() 右键
double_click() 鼠标双击
"""
from time import sleep
from selenium import webdriver
from selenium.webdriver import ActionChains

driver = webdriver.Chrome()
driver.get('https://www.baidu.com/')

# 定位目标

ele = driver.find_element_by_id('kw')

# 实例化 鼠标对象

action = ActionChains(driver)、

# 鼠标右键

action.context_click(ele)

# 鼠标双击

action.double_click(ele)

# 鼠标执行操作！！！不执行没效果

action.perform()

sleep(3)

driver.quit()
```



#### 4.2 鼠标拖拽

```
"""
鼠标操作：

# 鼠标拖拽

action.drag_and_drop(source， target)
"""
from time import sleep
from selenium import webdriver
from selenium.webdriver import ActionChains

driver = webdriver.Chrome()
driver.get('file:///D:/%E6%A1%8C%E9%9D%A2/page/drag.html')

red = driver.find_element_by_xpath('//*[@id="div1"]')
blue = driver.find_element_by_xpath('//*[@id="div2"]')

# 实例化鼠标

action = ActionChains(driver)

# 鼠标拖拽

action.drag_and_drop(red, blue)

# 鼠标执行

action.perform()

sleep(3)

driver.quit()
```

![请添加图片描述](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/1c872e1bbacc2df99d87e84db12268ae.gif)

#### 4.3 鼠标悬停 【重点】

```
"""
鼠标操作：

# 鼠标悬停 【重点】

action.move_to_element(element)
"""
from time import sleep
from selenium import webdriver
from selenium.webdriver import ActionChains

driver = webdriver.Chrome()
driver.get('https://www.baidu.com/')
driver.maximize_window()
ele = driver.find_element_by_id('s-usersetting-top')

# 实例化鼠标

action = ActionChains(driver)

# 鼠标悬停

action.move_to_element(ele)

# 鼠标执行

action.perform()

sleep(3)

driver.quit()
```

注意: selenium 框架虽然提供了 鼠标右键方法，但是没有提供选择右键菜单方法，可以通过键盘快捷键操作实现


### 五、键盘操作（不需要[实例化对象](https://so.csdn.net/so/search?q=%E5%AE%9E%E4%BE%8B%E5%8C%96%E5%AF%B9%E8%B1%A1&spm=1001.2101.3001.7020)）☆

1、说明：键盘对应的方法在Keys类中

```
# 包

from selenium.webdriver.common.keys import Keys
```

​    

2、快捷键（这里只讲windows操作系统的快捷键）：

 CONTROL: Ctrl键

 BACK_SPACE : 等价于 BACKSPACE （删除）

 其他：可以藏奥Keys底层的定义

3、应用

```
# 单键

element.send_keys(Keys.XXX)

# 组合键

element.send_keys(Keys.XXX, 'a') # 注意这里的组合键都是小写
```

```
"""
键盘操作
"""
from time import sleep
from selenium import webdriver
from selenium.webdriver.common.keys import Keys

driver = webdriver.Chrome()
driver.get('https://www.baidu.com/')

ele = driver.find_element_by_id('kw')
ele.send_keys('易烊千玺')
sleep(1)
ele.send_keys(Keys.BACK_SPACE)
sleep(1)

# 组合键 Ctrl + a 全选 ，注意这里的组合键都是小写

ele.send_keys(Keys.CONTROL, 'a')
sleep(1)
ele.send_keys(Keys.CONTROL, 'x')
sleep(1)
ele.send_keys(Keys.CONTROL, 'v')

sleep(3)

driver.quit()
```

![请添加图片描述](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/cd2511c040f30df3958cb9a83d6a04a0.gif)

### 六、元素等待

1、为什么要设置元素等待

 由于电脑配置或网络原因，在查找元素时，元素代码未在第一时间内被加载出来，而抛出未找到元素异常。

2、什么是元素等待

 元素在第一次未找到时，元素等待设置的时长被激活，如果在设置的有效时长内找到元素，继续执行代码，如果超出设置的时长未找打元素，抛出未找到元素异常。

3、元素等待分类

 隐式等待：针对全局元素生效；（讲这个）

 显示等待：稍微麻烦，有兴趣的可以下去了解，他是针对单个元素生效。

隐式等待方法：

```
driver.implicitly_wait(30) # 一般情况下设置30秒
```

 特色：

1. ```
   1. 针对所有元素生效。
   2. 一般情况下为前置必写代码(1.获取浏览器驱动对象；2. 最大化浏览器；3. 设置隐式等待)
   ```

   

```
"""
隐式等待
"""
from time import sleep
from selenium import webdriver
from selenium.webdriver.common.keys import Keys

driver = webdriver.Chrome()

# 1、获取浏览器驱动对象

driver.get('file:///D:/%E6%A1%8C%E9%9D%A2/page/%E6%B3%A8%E5%86%8CA%E7%AD%89%E5%BE%85.html')

# 2、窗口最大化

driver.maximize_window()

# 3、设置隐式等待

driver.implicitly_wait(30)
ele = driver.find_element_by_id('userA')
ele.send_keys('admin')

sleep(3)

driver.quit()
```



### 七、下拉框（需要实例化下拉框）

1、为什么单独使用下拉框？

 1)、如果option选项没有value值的化，css定位或其他定位就不太方便。

2、使用Select类

 1）、导包：`from selenium.webdriver.support.select improt Select`

 2）、实例化下拉框：`s = Select(element)`

 3）、调用方法：`s.select_by_index()`索引从0开始

3、Select类提供的方法

 1）、select_by_index() # 通过索引定位

 2）、select _by_value() # 通过value值

 3）、select_by_visible_text() # 显示文本

```
"""
Select类方法：
需要实例化下拉框元素定位
"""
from time import sleep

from selenium import webdriver
from selenium.webdriver.support.select import Select

driver = webdriver.Chrome()
driver.get('file:///D:/%E6%A1%8C%E9%9D%A2/page/%E6%B3%A8%E5%86%8CA.html')
ele = driver.find_element_by_id('selectA')

# 实例化下拉框

s = Select(ele)

# index 索引方法

s.select_by_index(1)
sleep(1)

# value 属性值选择目标元素

s.select_by_value('sz')
sleep(1)

# text 采用文本的方式选择目标信息

s.select_by_visible_text('A北京')

sleep(3)

driver.quit()
```

### 八、[弹出框](https://so.csdn.net/so/search?q=%E5%BC%B9%E5%87%BA%E6%A1%86&spm=1001.2101.3001.7020)

1、为什么要处理弹出框？

 一旦出现弹出框，如果不进行处理，则后续操作不可实现

2、弹窗分类

 系统弹窗：JS实现

 自定义弹窗：前端代码封装

3、对话框的分类：

 alert：警告框

 confirm：确认框

 prompt：提示框

4、如何处理

 系统弹窗：上面的对话框处理方式都一样；

```
步骤：
1、需要切换到对话框
  driver.switch_to.alert
2、处理对话框
  alert.text # 获取文本
  alert.accept() # 接受
  alert.dismiss() # 拒接
```

```
"""
系统弹窗：
切换对话框：driver.switch_to.alert
同意：alert.accept()
拒绝：alert.dismiss()
"""
from time import sleep

from selenium import webdriver
from selenium.webdriver.support.select import Select

driver = webdriver.Chrome()

driver.get('file:///D:/%E6%A1%8C%E9%9D%A2/page/%E6%B3%A8%E5%86%8CA.html')

driver.find_element_by_id('confirma').click()

# 切换对话框

alert = driver.switch_to.alert
print("文本内容是：", alert.text)
sleep(2)

# 拒绝

alert.dismiss()

# 同意

# alert.accept()

sleep(3)

driver.quit()
```



> 自定义弹窗，由于可以鼠标右击检查选项获取元素信息，所以出现自行已弹窗的时候，直接定义目标元素，并进行移除操作即可。

### 九、滚动条

1、为什么要是用滚动条？

 在一些特殊场景中，一些按钮是在页面最下角，需要使用滚动条拉到最底层。

2、操作步骤

Selenium框架中没有专门处理滚动条的方法，需要通过调用 `Js` 代码实现操作；

 1）、第一步：设置操作滚动条操作语句：`js_down="window.scollTo(0,1000)"`

 > 0:为左边距-----》水平滚动条

 > 1000: 为垂直滚动条

 2）、第二步：调用执行js方法，将设置js语句传入方法中

 > 方法：`driver.execute_script(js_down)`

```
"""
滚动条：selenium中没有滚动条方法，需要js代码实现
1、准备js代码："window.scrollTo(0, 1000)"
2、执行js代码：driver.execute_script(js的变量)
"""
from time import sleep
from selenium import webdriver

driver = webdriver.Chrome()

driver.get('file:///D:/%E6%A1%8C%E9%9D%A2/page/%E6%B3%A8%E5%86%8CA.html')
sleep(2)

# 1、准备js代码

js_down = "window.scrollTo(0, 1000)"

# 2、执行js代码

driver.execute_script(js_down)

sleep(3)

driver.quit()
```



### 十、切换frame表单 ☆

1、应用场景：

处于frame 中的元素，虽然可以获取元素信息，但是代码执行时无法定位元素，因此需要`先切换到frame`，再进行元素定位操作。

2、如何切换frame

方法：`driver.switch_to.frame("id/name/element")` 传入的是代表frame唯一的特征值

```
"""
frame的切换
"""
from time import sleep
from selenium import webdriver

driver = webdriver.Chrome()

driver.get('file:///D:/%E6%A1%8C%E9%9D%A2/page/%E6%B3%A8%E5%86%8C%E5%AE%9E%E4%BE%8B.html')

# 切换到frame

driver.switch_to.frame('idframe1')

# 在frame表单中填写信息

driver.find_element_by_id('userA').send_keys('admin')

sleep(3)

driver.quit()
```



#### 10.1 连续切换frame

说明：如果要连续切换frame必须要先回到默认页面，才能够实现下一个frame的切换

回到主页面的方法：`driver.switch_to.default_content()`

```
"""
需要默认切换到frame
方法：driver.switch_to.default_content()
"""
from time import sleep
from selenium import webdriver

driver = webdriver.Chrome()

driver.get('file:///D:/%E6%A1%8C%E9%9D%A2/page/%E6%B3%A8%E5%86%8C%E5%AE%9E%E4%BE%8B.html')

driver.switch_to.frame('idframe1')
driver.find_element_by_id('userA').send_keys('admin')

driver.switch_to.default_content()
driver.switch_to.frame('myframe2')
driver.find_element_by_id('userB').send_keys('admin4')

sleep(3)

driver.quit()
```



### 十一、多窗口的切换 ☆

1、为什么要切换多窗口

 页面是存在多窗口的，但是selenium默认焦点只会在`主窗口`上的所有元素，不切换窗口，就不能操作除主窗口以外的窗口内元素。

2、如何切换

每个窗口都有唯一的一个句柄值，那么我们就可以通过句柄值来完成窗口的切换操作

 方法：

 1）、`driver.current_window_handle` (获取当前的句柄值)

 2）、`driver.window_handles` （ 获取当前由driver启动所有窗口句柄）

 3）、`driver.switch_to.window(handle)` —> 切换窗口

```
"""
多窗口切换
driver.current_window_handle  获取当前的句柄值
driver.window_handles  获取driver启动的所有窗口句柄
driver.switch_to.window(handles[-1]) 切换窗口操作
"""
from time import sleep

from selenium import webdriver

driver = webdriver.Chrome()

driver.get('file:///D:/%E6%A1%8C%E9%9D%A2/page/%E6%B3%A8%E5%86%8C%E5%AE%9E%E4%BE%8B.html')

driver.find_element_by_id('ZCB').click()

# 1、获取当前的句柄值

# print("当前的句柄值是：", driver.current_window_handle)

# 2、

# 1).切换窗口操作,driver.window_handles 获取driver启动的所有窗口句柄

handles = driver.window_handles

# 2).切换窗口工作

driver.switch_to.window(handles[-1])
driver.find_element_by_id('userB').send_keys('admin9')

sleep(3)

driver.quit()
```

注意：这里的窗口切换也对应到了 close() 方法的作用，现在使用close（）就是关闭当前页面，如果还想重新操作原始页面，务必完成窗口切换。

### 十二、截图操作

使用的方法：

```
driver.get_screenshot_as_file(imgepath)
```

参数：

`imagepath`：为图片要保存的目录地址及文件名称

```
"""
截图：driver.get_screenshot_as_file(imgepath)
"""
from time import sleep

from selenium import webdriver

driver = webdriver.Chrome()

driver.get('https://www.baidu.com/')

driver.find_element_by_xpath('//*[@id="kw"]').send_keys('易烊千玺')

# 截图方法，建议使用png格式 ， ./为当前路径，  ../为上一级路径

driver.get_screenshot_as_file('./info.png')

sleep(3)

driver.quit()
```

注意：指定图片存放的路径，需要自己手动创建文件夹

### 十三、验证码

1、什么是验证码？

 一种随机生成的信息（文字，数字，图片）

2、验证码的作用？

 防止恶意请求

3、验证码的处理

 这边讲的是cookie解决

4、使用cookie 登录

 客户端登录账号后，将登录状态的想关 cookie
信息发给服务器保存，再发送去请求，携带cookie信息如果跟服务器保留的一致，则服务器认为客户端是登录状态。

5、这里实现自动登录的功能

 1）、准备工作，在客户端登录的状态下，获取cookie字段

![image-20220307191508407](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/53d1b8edc381f479a22d66ff2e96c3b8.png)

2、方法步骤：

```
1、整理cookie信息为字典数据，对应的是name和value，保存的一个变量中
2、调用方法添加cookie
  driver.add_cookie(cookie变量)

# 3、刷新页面 -->发送cookie给服务器验证

  driver.refresh()
```

cookie 的value就不给你们了，怕你们登录我的账号😂😂😂

* ```
  """
  验证码：
  {'name':'BDUSS',
  'value':'............................'}
  """
  from time import sleep
  
  from selenium import webdriver
  
  driver = webdriver.Chrome()
  
  driver.get('https://www.baidu.com/')
  driver.maximize_window()
  
  # 1、整理cookie信息为字典数据，对应的是name和value，保存的一个变量中
  
  cookie_value = {'name':'BDUSS',
  'value':'........................'}
  
  # 2、调用方法添加cookie
  
  driver.add_cookie(cookie_value)
  
  # 3、刷新页面 -->发送cookie给服务器验证
  
  driver.refresh()
  
  sleep(3)
  
  driver.quit()
  
  * 
  ```

  演示：

![请添加图片描述](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/bcec9436de19dd61975588b8c1755fd3.gif)

* * *

 终于把Selenium 给完结了，完结撒花❀❀❀❀❀❀❀❀❀❀
，这里面的方法都要掌握，然后可以找需求文档练习，铁汁们，觉得笔者写的不错的可以点个赞哟❤🧡💛💚💙💜🤎🖤🤍💟，收藏关注呗，你们支持就是我写博客最大的动力！！！！