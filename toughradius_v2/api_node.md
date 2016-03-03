## 区域节点查询


### 接口描述

- 查询系统区域节点

### 请求URL

- ` http://server:port/api/v1/node/query `
      
### 请求方式

- GET 或者 POST  

示例：

    GET /api/v1/node/query?sign=1BB40565D6C88276085719A5964BE3E0&node_id=1 HTTP/1.1

### 参数

| 参数名 | 必选 | 类型 | 说明 |
|---|:---|:---:|---:|
| node_id | 否 | string |区域ID |

### 返回结果

**返回示例：**

    {
      "code": 0,
      "msg": "success",
      "nodes": [
        {
          "id": 1,
          "node_name": "default",
          "node_desc": "默认区域"
        }
      ],
      "nonce": "1456377457",
      "sign": "91FBD7D83B5F9069E456E3DDCF1CCF9C"
    }

**返回结果描述：**

- code：返回结果码， 0 成功， 1 失败
- msg：返回消息
- nodes：区域节点列表，如果参数node_id不为空，则返回指定区域，若区域不存在，返回空。
- nonce：随机时间戳
- sign：消息签名


### 代码参考

- java

    import java.io.IOException;
    import org.apache.http.client.fluent.*;
    public class SendRequest
    {
        public static void main(String[] args) {
            sendRequest();
        }
        private static void sendRequest() {
            // node query (GET )
            try {
                // Create request
                Content content = Request.Get("http://127.0.0.1:1816/api/v1/node/query?sign=1BB40565D6C88276085719A5964BE3E0&node_id=1")
                // Fetch request and return content
                .execute().returnContent();
                // Print content
                System.out.println(content);
            }
            catch (IOException e) {
                System.out.println(e); 
            }
        }
    }

- php

    <?php
    // Get cURL resource
    $ch = curl_init();
    // Set url
    curl_setopt($ch, CURLOPT_URL, 'http://127.0.0.1:1816/api/v1/node/query?sign=1BB40565D6C88276085719A5964BE3E0&node_id=1');
    // Set method
    curl_setopt($ch, CURLOPT_CUSTOMREQUEST, 'GET');
    // Set options
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
    // Send the request & save response to $resp
    $resp = curl_exec($ch);
    if(!$resp) {
      die('Error: "' . curl_error($ch) . '" - Code: ' . curl_errno($ch));
    } else {
      echo "Response HTTP Status Code : " . curl_getinfo($ch, CURLINFO_HTTP_CODE);
      echo "\nResponse HTTP Body : " . $resp;
    }
    // Close request to clear up some resources
    curl_close($ch);


- python

    import requests
    def send_request():
        # node query
        # GET http://127.0.0.1:1816/api/v1/node/query
        try:
            response = requests.get(
                url="http://127.0.0.1:1816/api/v1/node/query",
                params={
                    "sign": "1BB40565D6C88276085719A5964BE3E0",
                    "node_id": "1",
                },
            )
            print('Response HTTP Status Code: {status_code}'.format(
                status_code=response.status_code))
            print('Response HTTP Response Body: {content}'.format(
                content=response.content))
        except requests.exceptions.RequestException:
            print('HTTP Request failed')

- go

    package main
    import (
        "fmt"
        "io/ioutil"
        "net/http"
    )
    func sendNodeQuery() {
        // node query (GET http://127.0.0.1:1816/api/v1/node/query?sign=1BB40565D6C88276085719A5964BE3E0&node_id=1)
        // Create client
        client := &http.Client{}
        // Create request
        req, err := http.NewRequest("GET", "http://127.0.0.1:1816/api/v1/node/query?sign=1BB40565D6C88276085719A5964BE3E0&node_id=1", nil)
        parseFormErr := req.ParseForm()
        if parseFormErr != nil {
            fmt.Println(parseFormErr)
        }
        // Fetch Request
        resp, err := client.Do(req)
        if err != nil {
            fmt.Println("Failure : ", err)
        }
        // Read Response Body
        respBody, _ := ioutil.ReadAll(resp.Body)
        // Display Results
        fmt.Println("response Status : ", resp.Status)
        fmt.Println("response Headers : ", resp.Header)
        fmt.Println("response Body : ", string(respBody))
    }


