# 说明
本文档为测试用例yaml编写的说明文档

## 用例说明

用例分为三部分

- ```testinfo``` 表示用例介绍
    - ```id``` 用例id
    - ```title``` 用例标题
    - ```info``` 前置条件
- ```testcase``` 用例的执行步骤
    - ```element_info: com.huawei.works.contact:id/title``` 元素
    -  ```find_type: id```  元素类型
        - ```id```
        - ```xpath```
        - ```css```
        - ```ids``` 需要增加```index```
        - ```index``` 和```ids```配合 
    - ```operate_type: click``` 操作
        - ```click```
        - ```swipe_down```
        - ```swipe_up```
        - ```get_value```
        - ```set_value``` 
        - ```msg``` 传给```set_value```关键字
        - ```adb_tab``` 使用adb中的tab命令点击元素,元素必须可识别，应用于悬浮层场景
        -  ```get_content_desc``` 无法切换到webview时，用此关键字
        - ```press_key_code``` 键盘触发事件，需要传```code```
        - ```code``` 传给```press_key_code```关键字
        - ```is_webview:1``` 为1表示切换到webview,为2表示切换到原生
        - ```其他关键字``` 用于定制一些特殊业务
    - ```is_time: 3``` 自定义暂停3秒
    - ```info: 点击动态列表第一条数据``` 操作步骤介绍
- ```check``` 检查点,支持多检查点
  - ```element_info: com.huawei.works.knowledge:id/browser_knowledge_history_text```
  - ```find_type: ids```
  - ```index: 0```
  - ```operate_type: get_value```
  - ```info: 查找是否存在历史记录```


## 实例

```buildoutcfg
testinfo:
    - id: test008
      title: 通讯录查看动态浏览记录
      info: 登陆打开weblink
testcase:
    - element_info: //*[@resource-id='com.huawei.works:id/w3_tab_content_layout']//android.widget.RadioButton[@text='通讯录']
      find_type: xpath
      operate_type: adb_tap
      info: 点击通讯录
    - element_info: com.huawei.works.contact:id/contact_item_name_layout
      find_type: ids
      index: 0
      operate_type: click
      info: 点击通讯录下的第一条数据
    - element_info: com.huawei.works.contact:id/title
      find_type: id
      operate_type: click
      info: 点击动态列表第一条数据
    - element_info: //*[@id="h5-scroll"]/div[1]/div/section[2]/div[1]/div
      find_type: xpath
      is_webview: 1 # 切换到webview
      operate_type: get_value
      info: 得到情页到标题
    - element_info: com.huawei.works.knowledge:id/vtb_img_left
      find_type: id
      is_webview: 2
      operate_type: click
      info: 点击返回按钮
    - element_info: com.huawei.works.contact:id/contact_vcard_back
      find_type: id
      operate_type: click
      info: 再次点击返回按钮
    - element_info: //*[@resource-id='com.huawei.works:id/w3_tab_content_layout']//android.widget.RadioButton[@text='知识']
      find_type: xpath
      operate_type: adb_tap
      info: 点击底部菜单知识
    - element_info: com.huawei.works.knowledge:id/vtb_img_right2
      find_type: id
      operate_type: click
      info: 点击首页历史记录按钮
check:
    - element_info: com.huawei.works.knowledge:id/browser_knowledge_history_text
      find_type: ids
      index: 0
      operate_type: get_value
      info: 查找是否存在历史记录
```


