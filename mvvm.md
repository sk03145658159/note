## mvvm    Vue

### 基于mvc   m---model      v---

### mvvm

mvvm  model--模型---数据   view---视图--模板---html和css

数据到试图   视图到数据   **双向数据绑定**（数据和视图一个改变均改变）

框架代表：angular和vue外哦（基于nodejs）

#### Vue

##### 引入vul.js文件

```vu
<div class="app">   在html中定义vul的作用范围块
    <input type="text" v-model="one">+<input type="text" v-model="two">=<span>{{one*1+two*1}}		</span>
     或者 <input type="text" v-model="one">+<input type="text" v-model="two">=<span                       v-text="one*1+two*1"></span>
    或者 <input type="text" v-model="one">+<input type="text" v-model="two">=<span>{{result()}}		</span>
     或者 <input type="text" v-model="one">+<input type="text" v-model="two">=<span                       v-text="result()"></span>
   <span v-text="three"></span>
</div>
<script>
    new Vue({    实例化vul对象
        el:".app",  确定作用范围
        data:{    为定义的属性赋值,json格式，表单内用v-model,表单外用{{}}(可以用v-text代替)
            one:0,   每个定义的属性都要赋值
            two:0,
            three:0
        }
        methods：{放逻辑部分，json格式（一个属性值改变，所有属性都会刷新一遍走一遍，效率差,当three值改变时，也会走一遍）
          result（）{
          	if(this.one>10){
               return this.one*1 + this.two*1
          	}else{
               return this.one*1 - this.two*1
          	}
          }
        }
         
         
         
       computed：{   放动态数据
          result（）{   不是方法，是动态数据，只有里面相关联的数据改变时才走一遍。当three值改变时，不会																					走一遍）
          	if(this.one>10){
               return this.one*1 + this.two*1
          	}else{
               return this.one*1 - this.two*1
          	}
          }
       }
       
       
       
       watch：{    自己监控属性值的变化，手动去监控某一个数据的变化(vul自动检测)
         one（after，before）{  参数before为修改前的值，after为修改后的值。
           console.log(111)
         }
       }
    })
</script>
<tr v-for="item in dates"> 循环
<input type="button" @click="result">点击事件
<input type="button" v-on:click="result">点击事件
<input type="button" @click="result($event)">返回事件对象
<div v-if="Math.random() > 0.5">   流程控制
  Now you see me
</div>
<div v-else>
  Now you don't
</div>
v-text
v-html
v-model：表单上的指定，目的是实现双向数据绑定
v-show
v-on=@
```

#### 自定义指令

```vu
 Vue.directive("focus",{   //自定义指令     focus自定义指令名
        inserted:function(ele,val){        inserted为指令发生的事件
            ele.focus()
        }
    })
自定义指令的调用v-focus    
    
    
// 注册
Vue.directive('my-directive', {
  bind: function () {},
  inserted: function () {},
  update: function () {},
  componentUpdated: function () {},
  unbind: function () {}
})

// 注册 (指令函数)
Vue.directive('my-directive', function () {
  // 这里将会被 `bind` 和 `update` 调用
})

// getter，返回已注册的指令
var myDirective = Vue.directive('my-directive')
```

#### 组件的制作

```vu
 Vue.component("car"函数名,{
        props:["dates"],接受参数(传参时传入列表型)         组件的制作,相当于函数
        template模板:`<div class="container">
        <table class="table table-bordered table-striped">
             <tr>
                <th>商品编号</th>
                <th>商品名称</th>
                <th>商品单价</th>
                <th>购买数量</th>
                <th>消费金额</th>
                <th>操作</th>
            </tr>
            <ul v-for="item in datas">
                <tr>
                    <td v-text="item.id"></td>
                    <td>{{item.name}}</td>
                    <td>{{item.grade}}</td>
                    <td>
                        <select class="form-control" v-model="item.num">
                            <option>1</option>
                            <option>2</option>
                            <option>3</option>
                            <option>4</option>
                            <option>5</option>
                        </select>
                    </td>
                    <td>{{item.grade*item.num}}</td>
                    <th><button class="btn btn-danger" type="button">删除</button></th>
                </tr>
            </ul>
            <tr>
                <td>商品总量：</td>
                <td></td>
                <td>消费总金额：</td>
                <td colspan="3"> </td>
            </tr>
        </table>
       
    </div>`,
    data(){    为函数格式
        return{
            datas:[
                {
                    id:1,
                    name:'安踏球鞋',
                    grade:260,
                    num:1
                },
                {
                    id:2,
                    name:'安踏球鞋',
                    grade:260,
                    num:1
                }
            ]}
        }
})
```

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <div>zhangsan</div>
</body>
</html>
<script>
    //Vue实现双向绑定的核心原理
    var temp=""
    var obj={}
    Object.defineProperty(obj,'name',{  //定义对象属性的方法
        // value:100,
        // writable:true,   //可更改,可设置(不设置，默认为不可更改)
        configurable:true,  //可删除（不设置，默认为不可删除）
        enumerable:true, //可枚举，遍历（不设置，默认为不可枚举）
        set:function(val){  //为属性设置值，一设置马上调用
            if(temp!=val){
                document.querySelector("div").innerHTML=val;            //这两个函数不能和语句一二一起使用
            }
            temp=val
        },
        get:function(){  //获取属性的值，一获取就调用。  属性最后的值取决于temp
            return temp
        }
    })
    obj.name="zhangsan"
   console.log(obj.name)
   obj.name="lisi"
   console.log(obj.name)
</script>
```



努力是有目标的自觉奋斗，而忙碌是被别人毫无目地的拖着走

#### localStorage本地存储     （Application中）

localStorage.aa="bb"  /[1,2,3,4]/fubction/{}/[{}]          添加存储变量

localStorage.aa="cc"    修改

localStorage.setItem("aa","bb")          添加存储变量

localStorage.removeItem("aa","bb")    删除存储变量

localStorage.clear()  清楚所有数据

均已字符串的形式存储

- [ ] 存储是转换为字符串形式JSON.stringify()
- [ ] 读取是转换会json格式JSON.parse()