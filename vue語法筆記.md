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
### 表達式
```
1.在表達式中使用反引號
<p>{{ `${name}123` }}</p>
2.在表達式中使用js語法
<p>{{ text.split('').reverse().join('') }}</p>
3.在表達式中呼叫函式
<p>{{ say('toad') }}</p>
```
### v-pre取消編譯
