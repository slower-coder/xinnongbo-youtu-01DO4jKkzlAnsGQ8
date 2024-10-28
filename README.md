
### 1\. 解析器源码分析


注意：以下源码为了方便理解已进行简化，只保留了解析器相关的代码



```
# 视图函数：
class MyView(APIView):
    def post(self, request):
        print(self.request.data)  # 触发解析流程
        return Response("ok")

```

##### 解析并获取数据的源码分析：


![image](https://img2024.cnblogs.com/blog/3514987/202410/3514987-20241027195404603-1254521984.png)
![image](https://img2024.cnblogs.com/blog/3514987/202410/3514987-20241027195819719-1224179082.png)


##### 获取解析器的源码分析：


![image](https://img2024.cnblogs.com/blog/3514987/202410/3514987-20241027200557337-159689647.png)
![image](https://img2024.cnblogs.com/blog/3514987/202410/3514987-20241027201202662-504198260.png)


##### 解析器解析数据的源码分析（以JSONParser为例）：


![image](https://img2024.cnblogs.com/blog/3514987/202410/3514987-20241027201925342-602898675.png)


### 2\.实践应用



```
# 视图类中：
class MyView(APIView):
    # 指定解析器(如果未指定则用默认的parser_classes=[MultiPartParser, JSONParser, FormParser]
    parser_classes = [JSONParser, FormParser]  # 只能解析JSON和form表单数据

    # 匹配解析器的方法(默认使用该类中的方法来匹配解析器，即使不显式地写出来也能生效）
    content_negotiation_class = DefaultContentNegotiation

    def post(self, request):
        print(self.request.data)
        return Response("ok")

```

 本博客参考[milou加速器](https://jiechuangmoxing.com)。转载请注明出处！
