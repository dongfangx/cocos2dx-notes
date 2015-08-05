#HttpClient

## 引入头文件
```
#include "network/HttpClient.h"
using namespace cocos2d::network;
```
## get
```
HttpRequest* request = new HttpRequest();
request->setUrl("http://www.baidu.com");
request->setRequestType(HttpRequest::Type::GET);
request->setResponseCallback(CC_CALLBACK_2(HelloWorld::onHttpRequestCompleted,this));
request->setTag("GET test");
cocos2d::network::HttpClient::getInstance()->send(request);
request->release();
```

## post
```
HttpRequest* request = new HttpRequest();
request->setUrl("http://httpbin.org/post");
request->setRequestType(HttpRequest::Type::POST);
request->setResponseCallback(CC_CALLBACK_2(HelloWorld::onHttpRequestCompleted,this));

// write the post data
const char* postData = "visitor=cocos2d&TestSuite=Extensions Test/NetworkTest";
request->setRequestData(postData, strlen(postData));
request->setTag("POST test");
cocos2d::network::HttpClient::getInstance()->send(request);
request->release();
```

## 回调
```
void HelloWorld::onHttpRequestCompleted(HttpClient *sender, HttpResponse *response)
{
    if (!response)
    {
        return;
    }    

    // You can get original request type from: response->request->reqType
    if (0 != strlen(response->getHttpRequest()->getTag()))
    {
        log("%s completed", response->getHttpRequest()->getTag());
    }    
    int statusCode = response->getResponseCode();
    char statusString[64] = {};
    sprintf(statusString, "HTTP Status Code: %d, tag = %s", statusCode, response->getHttpRequest()->getTag());
    _labelStatusCode->setString(statusString);
    log("response code: %d", statusCode);    
    if (!response->isSucceed())
    {
        log("response failed");
        log("error buffer: %s", response->getErrorBuffer());
        return;
    }
    // dump data
    std::vector<char> *buffer = response->getResponseData();
    printf("Http Test, dump data: ");
    for (unsigned int i = 0; i < buffer->size(); i++)
    {
        printf("%c", (*buffer)[i]);
    }
    printf("\n");
}

```

## 备注:
```
//Android 在应用程序的Manifest 中增加权限
<uses-permission android:name=”android.permission.INTERNET” />
```
