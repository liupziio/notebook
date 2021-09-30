# 一、el-input类型

+ number 类型

当需要验证的字段是数字类型的时候，需要使用 v-model.number 来绑定，否则验证的时候会当做字符串处理，结果就无法验证

```js
 <el-input    v-model.number="tax.salary"></el-input>
1
```

rules里面：

```js
           salary: [{required: true, message: '请输入工资',type:'number', trigger: 'blur'}],
```

+ 去除掉上下小箭头

```css
input::-webkit-outer-spin-button,input::-webkit-inner-spin-button{
  -webkit-appearance: none !important;
  -moz-appearance: none !important;
  -o-appearance: none !important;
  -ms-appearance: none !important;
  appearance: none !important;
  margin: 0;
}
```



# 二、rules 验证

## 1、动态绑定rules 验证

+ 如果使用**v-if**隐藏的，不会去验证

```js
 :rules="radio == '1' ? rules.levelIconColor : [{ required: false }]"
```



## 2、自定义rules 验证

+ 在data中定义自定义验证

```js
 data() {
     //在data中设置验证规则
        let validID = (rule, value, callback) => {
          let _IDRe18 = /^([1-6][1-9]|50)\d{4}(18|19|20)\d{2}((0[1-9])|10|11|12)(([0-2][1-9])|10|20|30|31)\d{3}[0-9Xx]$/;
          let _IDre15 = /^([1-6][1-9]|50)\d{4}\d{2}((0[1-9])|10|11|12)(([0-2][1-9])|10|20|30|31)\d{3}$/; // 校验身份证：
          if (value !== "" || value !== undefined) {
            if (value.length === 15) {
              if (!_IDre15.test(value)) {
                callback(new Error("身份证号码不正确"));
              } else {
                callback();
              }
            } else {
              if (!_IDRe18.test(value)) {
                callback(new Error("身份证号码不正确"));
              } else {
                callback();
              }
            }
          }
        };
     
     
     rules: {
           userid: [
              { required: true, message: "请输入身份证号", trigger: "blur" },
               #这里写入自定义验证规则 "validID" 对象
              { validator: validID, trigger: "blur" },
              // { required: true, message: "请选择身份证号", trigger: "blur" },

            ],
     }
```



# 三、样式

## 1、table滚动table头部错位问题

+ 更改滚动条样式
  + 让头部的宽度等于100%减去滚动条的宽度
  + 放在app.vue全局上可以不用 !important
    + 以防单独页面可以使用 !important

```js
.el-table__body-wrapper::-webkit-scrollbar {
  width: 11px !important;
  height: 11px !important;
}
.el-table__body-wrapper::-webkit-scrollbar-thumb {
  background-color: #ddd !important;
  border-radius: 6px;
}
.el-table {
  width: calc(100% - 11px) !important;
  .el-table__header-wrapper {
    width: calc(100% - 11px) !important;
  }
}
```

