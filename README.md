## 迴圈 [v-for](https://github.com/4080E68/Vue/blob/master/README.md#v-for%E8%AA%9E%E6%B3%95)
## 資料綁定  [v-bind](https://github.com/4080E68/Vue/blob/master/README.md#v-bind-%E8%B3%87%E6%96%99%E7%B6%81%E5%AE%9A)

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
### 切換 Class
```
如果遇到class名稱當中有-號須將class名稱用字串符號包住
可在值上定義一個變數，回傳true或是false
isTransform: true,
boxColor: false,
:class="{ rotate : isTransform ,'bg-danger': boxColor }

也可使用object方式綁定class
:class="ObjectClass"
ObjectClass:{
        rotate: true, 
        'bg-danger': true
}

陣列寫法
:class="arrayClass"
透過v-on傳入class樣式
v-on:click="addClass(['btn-primary', 'disabled'])//需使用陣列格式
addClass(arr) {
  this.arrayClass.push(...arr);
}
```

# v-model

##### 單選
```
如果再checkbox上綁定v-model會以boolean方式回傳
<input type="checkbox" class="form-check-input" id="check1" v-model="checkAnswer">

使用true-value、false-value達到三元運算子效果
因為回傳得一定是true或是false所以可以使用true-value
<input type="checkbox" class="form-check-input" id="check2" 
    v-model="checkAnswer2"
    true-value="吃飽了"
    false-value="還沒">
```

##### 複選
```
<p>{{ checkAnswer3.join(' ') }}</p>
join(以何種方式區隔)會將陣列中所有的元素連接、合併成一個字串，並回傳此字串。
使用複選時須加上value的值，因為在複選時是使用陣列的方式回傳
而回傳的值是取決於value，所以在使用前也需宣告一個空的陣列。

<div class="form-check">
    <input type="checkbox" class="form-check-input" id="check3" value="蛋餅" v-model="checkAnswer3">
    <label class="form-check-label" for="check3">蛋餅</label>
  </div>
  <div class="form-check">
    <input type="checkbox" class="form-check-input" id="check4" value="蘿蔔糕" v-model="checkAnswer3">
    <label class="form-check-label" for="check4">蘿蔔糕</label>
</div>
```
##### radio 單選框
```
在radio裡面因為只能單選，所以在回傳值是會直接將原有得值取代
也是使用value作為回傳的值
<input type="radio" class="form-check-input" id="radio1" value="蛋餅" v-model="radioAnswer">
```
##### select選擇框
```
在select裡面也是使用value來當回傳值
可以搭配v-for將option顯示
<option :value="item.name" v-for="(item, index) in products" :key="item.name">{{item.name}}</option>

將需要顯示的選項value設為空字串在設定disabled
<option value="" disabled>說吧，你要吃什麼？</option>
```
##### select多選框
```
同上，但是需要再加上multiple
按下ctrl時就可以複選
```
##### 修飾符
```
v-model.lazy 用戶需按下enter或點擊輸入框外面資料才會傳遞回去
v-model.number 將輸入的資料型態改為數字，但如果type為text時需要輸入的第一個字為數字才會把型態轉為number
v-model.trim 將前後空白都刪除，常使用在email格式。
```
