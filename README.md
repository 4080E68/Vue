##迴圈 [v-for](https://github.com/4080E68/Vue/edit/master/README.md#v-for%E8%AA%9E%E6%B3%95)
##資料綁定  [v-bind](https://github.com/4080E68/Vue/edit/master/README.md#v-bind-%E8%B3%87%E6%96%99%E7%B6%81%E5%AE%9A)
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
# v-if、v-else-if、v-else
```
語法:<v-if="判斷式">
<li v-if="item.price <= 35">
   {{ item.name}} / {{ item.price }} 元
</li>
```
### v-if盡量不要跟v-for一起使用需分開!
```
如需同時使用請使用template方式
<template v-for="(item, key) in products" v-bind:key="item.name">
              <li v-if="item.price <= 35">
                {{ item.name}} / {{ item.price }} 元
              </li>
</template>
```
# v-bind 資料綁定
### 縮寫 :<html標籤>
```
綁定src v-bind:src="breakfastShop.imgUrl" 或是 :src="breakfastShop.imgUrl"
```
### 變數綁定
```
<button type="submit" :disabled="isFull">送出</button>
當中的disabled會判斷如果傳入的是true則顯示disabled反之則相反
```
### 搭配 v-for
```
也可在for迴圈裡面使用
<tr v-for="item in products" :key="item.imgUrl">
  <img :src="item.imgUrl" class="square-img" alt="">
</tr>
```
### 透過綁定動態切換圖片大小
```
這裡需使用反引號帶入變數
<input type="range" min="100" max="1000" v-model="imageSize">
<img :src="`${breakfastShop.resizeImg}&w=${imageSize}`" alt="">
```
### 動態屬性綁定
```
先在button判斷disabled的值
<button type="button" v-on:click="dynamic = dynamic === 'disabled' ? 'readonly':'disabled'">切換為{{ dynamic }}</button>
再裡用中括號直接將判斷的值寫入為HTML格式
<input type="text" :[dynamic] :value="name">
```
