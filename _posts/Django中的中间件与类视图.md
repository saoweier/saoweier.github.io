## 类视图
 

 - 函数视图：以函数的方式定义的视图称为函数视图
	类视图：以类的方式定义的视图称为类视图
 - 代码可读性好
	类视图相对于函数视图有更高的复用性
	因此大部分视图都使用类进行封装。
	

```python
from django.views import View
class ClassView(View):
    """类视图的介绍"""

    def get(self, request):
        """get请求方法"""
        print('get请求方法进次函数')
        return HttpResponse('get请求方法')

    def post(self, request):
        """post请求方法进此函数"""
        print('post请求方法')
        return HttpResponse('post请求方法')
    """
	在url中配置
	"""
	urlpatterns = [
    url(r"^classview/$", views.ClassView.as_view())
    #ClassView是一个类 需要调用Django自带的as_view方法转换为view

]
```
## 中间件

 - 中间件
Django中的中间件是一个轻量级、底层的插件系统，可以介入Django的请求和响应处理过程，修改Django的输入或输出。中间件的设计为开发者提供了一种无侵入式的开发方式，增强了Django框架的健壮性。

我们可以使用中间件，在Django处理视图的不同阶段对输入或输出进行干预。

```python
#先在子应用文件下新建(自定义).py文件
# 自定义中间键
def outer(fuc):
    print('调用前')
    def inner(*args, **kwargs):
        print('执行前')
        data = fuc(*args, **kwargs)
        print(' 执行后')
        return data
    return inner
#2. settings.py的middleware下面加入自定义的中间件
'user1.middlewares.outer'  # 自定义中间件
```
![中间件的执行顺序](https://img-blog.csdnimg.cn/20200603180129729.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1NPUllVU0hJS0lOQU1J,size_16,color_FFFFFF,t_70).![在这里插入图片描述](https://img-blog.csdnimg.cn/20200603180659121.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1NPUllVU0hJS0lOQU1J,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200603181245183.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1NPUllVU0hJS0lOQU1J,size_16,color_FFFFFF,t_70)
