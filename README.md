# autocomplete

# 使用说明

这是一个 uniapp 组件

标签（空格分隔）： autocomplete
在标签里引入

```html
<str-autocomplete :stringList="stringList" :importvalue="title" @select="selectOne" highlightColor="#FF0000" v-model="title"></str-autocomplete>
```

---

代码块引入

```javascript
import strAutocomplete from '@/components/str-autocomplete/str-autocomplete.vue'
export default {
  components: {
    strAutocomplete
  },
  data() {
    return {
      title: 'Hello',
      stringList: [
        'apple',
        'string',
        'delicious',
        'everything',
        'somethingWrong',
        '中古国'
      ]
    }
  },
  onLoad() {},
  methods: {
    selectOne(opt) {
      this.title = opt
      console.log(opt)
    },
    changeTitle(text) {
      this.title = text
    }
  }
}
```

# 更新内容
# 2020.4.16
修改了匹配文字时引发的undefined问题
在例子中添加了输入文字触发的事件 @change="textChange"
# 2019.12.5
修改了由于输入框失去焦点导致点击选项没有生效的bug
# 2019.11.18
输入框失去焦点时下拉框会消失
# 2019.10.31
默认添加了忽略大小写匹配，如果严格匹配不忽略大小写，需要在引用时添加lowerAndUp="no"，例如：
```
<str-autocomplete :stringList="stringList" :importvalue="title" lowerAndUp="no" @select="selectOne" highlightColor="#FF0000" v-model="title"></str-autocomplete>
```

# 2019.7.11

  1. 修改了选择同样值value不会更新的问题
  2. 添加了属性importvalue，使importvalue与v-model相同的值可以在父组件修改value值
  3. app测试中，model值不能随选择修改，需要在选择事件select的回调函数中修改model值，例如
      ```
      selectOne(opt) {
				this.title = opt
        console.log(opt)
      },
      ```
  4. 修改插件中的部分let为const

# 2019.6.5

下拉单添加点击事件
