# Httpclient技术

在后端开发过程中，后端服务不一定部署在一台服务器上，所以我们需要一种技术可以实现后端调用其他后端的服务，这种调用被称为RPC（远程过程调用），如下图所示： 
![这里写图片描述](https://img-blog.csdn.net/20180421222956771?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM4OTA0NzAw/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70) 
HttpClient 是 Apache Jakarta Common 下的子项目，用来提供高效的、最新的、功能丰富的支持 HTTP 协议的客户端编程工具包，并且它支持 HTTP 协议最新的版本和建议。拥有以下几个主要功能：

-  实现了所有 HTTP 的方法（GET,POST,PUT,HEAD 等）

-  支持自动转向

-  支持 HTTPS 协议

-  支持代理服务器等 
  通过使用Httpclient可以实现以下过程： 
  ![这里写图片描述](https://img-blog.csdn.net/20180421223108919?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM4OTA0NzAw/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70) 
  根据Httpclient的使用方法，先创建Httpclient的实例，通过连接地址创建连接方式（GET、POST等）的实例，执行创建好的实例接收返回值，处理好返回值后释放连接。

  核心代码（JSON格式）：

```
//GET
    public static String DoGet(String url){
        //设置连接配置
        RequestConfig requestConfig = RequestConfig.custom().setConnectTimeout(5000)
                .setSocketTimeout(5000).setConnectionRequestTimeout(5000).build();
        //创建HttpClient实例
        HttpClient httpClient = HttpClientBuilder.create().build();
        //创建GET的连接方式实例
        HttpGet httpGet = new HttpGet(url);
        //配置请求头
        httpGet.addHeader("content-type", "application/json");
        httpGet.addHeader("Accept", "application/json");
        httpGet.setConfig(requestConfig);
        try{
            //接收响应信息
            HttpResponse httpResponse = httpClient.execute(httpGet);
            //如果响应信息正确返回响应体信息
            if(httpResponse.getStatusLine().getStatusCode() == 200){
                return EntityUtils.toString(httpResponse.getEntity());
            }else {
                return "{\"message\":\"请求失败\"}";
            }
        }catch (IOException e){
            return "{\"message\":\"IOException异常\"}";
        }finally {
            //释放连接
            httpGet.releaseConnection();
        }
    }
```

```
//POST
    public static String DoPost(String url, Chain chain){
        //设置连接配置
        RequestConfig requestConfig = RequestConfig.custom().setConnectTimeout(5000)
                .setSocketTimeout(5000).setConnectionRequestTimeout(5000).build();
        //创建HttpClient实例
        HttpClient httpClient = HttpClientBuilder.create().build();
        //创建POST的连接方式实例
        HttpPost httpPost = new HttpPost(url);
        //配置请求头
        httpPost.addHeader("content-type", "application/json");
        httpPost.addHeader("Accept", "application/json");
        httpPost.setConfig(requestConfig);
        try{
            //添加请求题信息
            String jsonString = JSON.toJSONString(chain);
            System.out.println(jsonString);
            StringEntity entity = new StringEntity(jsonString);
            httpPost.setEntity(entity);
            //接收响应信息
            HttpResponse httpResponse = httpClient.execute(httpPost);
            //如果响应信息正确返回响应体信息
            if(httpResponse.getStatusLine().getStatusCode() == 200){
                return EntityUtils.toString(httpResponse.getEntity());
            }else {
                return "{\"message\":\"请求失败\"}";
            }
        }catch (IOException e){
            return "{\"message\":\"IOException异常\"}";
        }finally {
            //释放连接
            httpPost.releaseConnection();
        }
    }
```

