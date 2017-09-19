# vue-captcha

Component (es6) Captcha for Vue.js

# Version

  - npm v1.0.2 (latest) [HERE](https://www.npmjs.com/package/vue-captcha)

# Demo

The demo page is [HERE](http://rafaelbm91.github.io/vue-captcha/demo.html).

# Requirements

- [Vue.js](https://github.com/yyx990803/vue) `^2.0.0`
- [uuid](https://www.npmjs.com/package/uuid) `^4.7.0`
- [font-awesome](http://fontawesome.io/)     `^3.1.0`

# Instllation

## npm

```shell
$ npm install --save vue-captcha
```

# Usage

```html
<template>
  <div class="form">
    <div class="row">
      <div><strong>Default</strong></div>
      <my-captcha :callSuccess="captchaBtn"></my-captcha>
      <button class="button" v-bind:disabled="btndis" v-on:click="clicked">Submit</button>
    </div>
    <div class="row">
      <div><strong>Change: color </strong></div>
      <my-captcha :callSuccess="captchaOk" color="green"></my-captcha>
    </div>
    <div class="row">
      <div><strong>Change: color / resolve (only text) </strong></div>
      <my-captcha :callSuccess="captchaOk" color="orange" resolve="text"></my-captcha>
    </div>
    <div class="row">
      <div><strong>Change: color / resolve (only digit) </strong></div>
      <my-captcha :callSuccess="captchaOk" color="purple" resolve="digit"></my-captcha>
    </div>
    <div class="row">
      <div><strong>Change: color / mode (math) </strong></div>
      <my-captcha :callSuccess="captchaOk" color="blue" mode="math"></my-captcha>
    </div>
    <div class="row">
      <div><strong>Change: color / mode (math) / resolve (only text) </strong></div>
      <my-captcha :callSuccess="captchaOk" color="black" mode="math" resolve="text"></my-captcha>
    </div>
    <div class="row">
      <div><strong>Change: color / mode (math) / resolve (only digit) </strong></div>
      <my-captcha :callSuccess="captchaOk" color="red" mode="math" resolve="digit"></my-captcha>
    </div>
  </div>
</template>

<script>

import myCaptcha from 'vue-captcha'

export default {
  name: 'form',
  data () {
    return {
      btndis: true
    }
  },
  methods: {
    captchaOk () {
      console.log('captcha ok.!')
    },
    captchaBtn () {
     this.btndis = false
    },
    clicked () {
      alert('button active.!')
    }
  },
  components: {
    'my-captcha': myCaptcha
  }
}
</script>

<style scope>
  .form {
    margin: 10px;
  }
  .row {
    margin: 10px;
  }
  .button {
    margin-top: 5px;
    background-color: #1D9D74;
    border: 1px solid transparent;
    border-radius: 3px;
    border-color: #dbdbdb;
    text-align: center;
    font-size: 1em;
    height: 2.25em;
    line-height: 1.5;
    color: white;
    cursor: pointer;
    padding-bottom: calc(0.375em - 1px);
    padding-left: calc(0.625em - 1px);
    padding-right: calc(0.625em - 1px);
    padding-top: calc(0.375em - 1px);
  }
  .button[disabled] {
    cursor: not-allowed;
    opacity: 0.6;
  }  
</style>
```

# API

- callSuccess 

  * call Function when Captcha is successful

```javascript

type: Function,
required: true

```

- color

  * apply color to different components in the Captcha  

```javascript

type: String
reuired: false
default: '#1D9D74'

```

- mode
  
  * change the way in the option to question

```javascript

type: String
required: false
default: 'text' // 'text' -> alphanumeric | 'math' -> operations math

```

- resolve

  * change the way the solve

```javascript

type: String
required: false
default: 'all' // 'all' -> written and digit | 'text' -> only written | 'digit' -> only digit

```

### prop (Function CallBack -success- )

```javascript

captchaOk = () => {
  console.log('captcha ok.!')
}

```

```html

<my-captcha :callSuccess="captchaOk"></my-captcha>

```

# License

[The MIT License](http://opensource.org/licenses/MIT)

Copyright (c) 2017-present, Rafael Briceño @rafaelbm91
