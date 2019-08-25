# dd-store - 钉钉E应用状态管理

## 安装

``` js
npm i dd-store --save
```

## 使用

参考样例：[Github](https://github.com/linjc/dd-store/tree/master/examples)

页面内使用

``` js
import create from '../../../src/create'
import store from '/store'

// 使用create.Page方法创建页面
create.Page({

  store,

  data: {
    // 按需注入共享状态（与store.data内字段同名即可），可以直接修改store值并通过this.update()方式更新
    // 此处只定义需要的状态，设置的默认值无效，如需设置请在store.data内设置
    userName: null,
    corpName: null,

    // 定义store.data没有的字段，则默认为页面私有状态，只能使用默认的this.setData(obj)方式更新
    pageName: 'Index页面'
  },

  handleChange() {
    this.store.onChange()
  },

  toTestPage() {
    dd.navigateTo({ url: '/pages/test/test' })
  }

});

```

组件内使用
``` js
import create from '../../../src/create'

// 使用create.Component方法创建组件，会自动从父级页面注入store，不需要手动注入
create.Component({
  data: {
    // 按需注入共享状态（与store.data内字段同名即可），可以直接修改store值并通过this.update()方式更新
    // 此处只定义需要的状态，设置的默认值无效，如需设置请在store.data内设置
    userList: null,
    deptList: null,

    // 定义store.data没有的字段，则默认为组件私有状态，只能使用默认的this.setData(obj)方式更新
    commName: 'comm-a组件'
  },

  methods: {
    handleChange() {
      const ran = Math.floor(Math.random() * 10000)
      this.store.data.userList[0].name = '刘备' + ran
      this.store.data.deptList[0].name = '产品经理' + ran
      this.update()
    }
  },
});
```
