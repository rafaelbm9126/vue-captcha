# vue-captcha

Component (es6) Captcha for Vue.js

# Demo

The demo page is [HERE](http://rafaelbm91.github.io/vue-captcha/demo.html).

# Requirements

- [Vue.js](https://github.com/yyx990803/vue) `^2.0.0`
- [uuid](https://www.npmjs.com/package/uuid) `^4.7.0`
- [font-awesome](http://fontawesome.io/)     `^3.1.0`

# Instllation

## npm

```shell
$ npm install vue-captcha
```

# Usage

```html
<script>

import myCaptcha from 'vue-captcha'

export default {
	methods: {
		captchaOk () {
			console.log('captcha ok.!')
		}
	},
  components: {
    'my-captcha': myCaptcha
  }
}
</script>
<template>
  <div class="form">

    <div class="row">
      <my-captcha :callSuccess="captchaOk" color="orange" ></my-captcha>
    </div>

  </div>
</template>
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
default: "#1D9D74"

```

### prop

```javascript

captchaOk = () => {
	console.log('captcha ok.!')
}

```

```html

<my-captcha :callSuccess="captchaOk" ></my-captcha>

```


# License

[The MIT License](http://opensource.org/licenses/MIT)
