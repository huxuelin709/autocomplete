# autocomplete

# 使用说明

这是一个 uniapp 组件

标签（空格分隔）： autocomplete
在标签里引入

```html
<str-autocomplete
  :stringList="stringList"
  @select="selectOne"
  highlightColor="#FF0000"
  v-model="title"
></str-autocomplete>
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
      console.log(opt)
    }
  }
}
```

# 更新内容

# 2019.6.5

下拉单添加点击事件
