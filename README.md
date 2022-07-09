# 表達式
```
1.在表達式中使用反引號
<p>{{ `${name}123` }}</p>
2.在表達式中使用js語法
<p>{{ text.split('').reverse().join('') }}</p>
3.在表達式中呼叫函式
<p>{{ say('toad') }}</p>
```
### v-pre取消編譯
```
<p v-pre>這段文字不會被轉譯：{{ name }}在{{ position }}吃早餐</p>
```
### v-html 寫入html格式
```
<div v-html="rawHtml"></div>
```
### v-once 改為單向綁定
```
這樣在操作資料時畫面上的資料不會一起更動
<h3>單次綁定</h3>
  <p v-once>{{ name }}在{{ position }}吃早餐</p>
  <input type="text" v-model="name">
```


# v-for語法

### v-for="item,index in 物件" v-bind:key="item.綁定目標"
```
<li v-for="(item, key) in products" v-bind:key="item.name">
   {{ key }} - {{ item.name}} / {{ item.price }} 元
</li>
```
### 三元運算值
```
if另類寫法
{{item.vegan ? 'true' : 'false'}}
```
### 在template使用v-for
```
在遇到不同階層需要使用for時可以在最外層加入template
以此讓for迴圈的範圍擴大
EX:
<template v-for="(item, index) in products" :key="item.name">
                <tr>
                  <th rowspan="2">{{index + 1}}</th>
                  <td colspan="2">
                    {{item.name}}
                  </td>
                </tr>
                <tr>
                  <td>
                    {{item.price}}
                  </td>
                  <td>
                    {{item.vegan ? '素食' : '不可素食'}} 
                    <!-- 三元運算值 -->
                  </td>
                </tr>
</template>
```
