<template>
  <div id="VueCaptcha" class="vue-captcha" v-bind:style="`border: 1px solid ${color};`">
		<div class="content-captcha">
			<canvas class="vue-captcha-img" width="150" height="25"></canvas>
		</div>
		<div class="content-text" v-show="opc === 1 && !auth">
			<input type="text" v-on:keyup="inputText" v-model="text" placeholder="insert key..." />
		</div>
		<div class="content-ok" v-show="auth" v-bind:style="`background-color: ${color};`">
			<small> <i class="fa fa-thumbs-up"></i> success.!</small>
		</div>
		<div class="content-fixed" v-show="opc === 2 && !auth" v-bind:style="`top:${contenTextTop}px;left:${contenTextLeft}px;`">
			<table class="vue-captcha-table" cellspaceng="0">
				<tr v-show="mode === 'text'">
					<td class="vue-captcha-table-item" v-on:click="selectItem">1</td>
					<td class="vue-captcha-table-item vue-captcha-table-item-center" v-on:click="selectItem">2</td>
					<td class="vue-captcha-table-item" v-on:click="selectItem">3</td>
					<td class="vue-captcha-table-item vue-captcha-table-item-center" v-on:click="selectItem">4</td>
					<td class="vue-captcha-table-item" v-on:click="selectItem">5</td>
					<td class="vue-captcha-table-item vue-captcha-table-item-center" v-on:click="selectItem">6</td>
					<td class="vue-captcha-table-item" v-on:click="selectItem">7</td>
					<td class="vue-captcha-table-item vue-captcha-table-item-center" v-on:click="selectItem">8</td>
					<td class="vue-captcha-table-item" v-on:click="selectItem">9</td>
					<td class="vue-captcha-table-item vue-captcha-table-item-right" v-on:click="selectItem">0</td>
				</tr>
				<tr v-show="mode === 'text'">
					<td class="vue-captcha-table-item" v-on:click="selectItem">q</td>
					<td class="vue-captcha-table-item vue-captcha-table-item-center" v-on:click="selectItem">w</td>
					<td class="vue-captcha-table-item" v-on:click="selectItem">e</td>
					<td class="vue-captcha-table-item vue-captcha-table-item-center" v-on:click="selectItem">r</td>
					<td class="vue-captcha-table-item" v-on:click="selectItem">t</td>
					<td class="vue-captcha-table-item vue-captcha-table-item-center" v-on:click="selectItem">y</td>
					<td class="vue-captcha-table-item" v-on:click="selectItem">u</td>
					<td class="vue-captcha-table-item vue-captcha-table-item-center" v-on:click="selectItem">i</td>
					<td class="vue-captcha-table-item" v-on:click="selectItem">o</td>
					<td class="vue-captcha-table-item vue-captcha-table-item-right" v-on:click="selectItem">p</td>
				</tr>
				<tr v-show="mode === 'text'">
					<td class="vue-captcha-table-item" v-on:click="selectItem">a</td>
					<td class="vue-captcha-table-item vue-captcha-table-item-center" v-on:click="selectItem">s</td>
					<td class="vue-captcha-table-item" v-on:click="selectItem">d</td>
					<td class="vue-captcha-table-item vue-captcha-table-item-center" v-on:click="selectItem">f</td>
					<td class="vue-captcha-table-item" v-on:click="selectItem">g</td>
					<td class="vue-captcha-table-item vue-captcha-table-item-center" v-on:click="selectItem">h</td>
					<td class="vue-captcha-table-item" v-on:click="selectItem">j</td>
					<td class="vue-captcha-table-item vue-captcha-table-item-center" v-on:click="selectItem">k</td>
					<td class="vue-captcha-table-item" v-on:click="selectItem">l</td>
				</tr>
				<tr v-show="mode === 'text'">
					<td class="vue-captcha-table-item"></td>
					<td class="vue-captcha-table-item" v-on:click="selectItem">z</td>
					<td class="vue-captcha-table-item vue-captcha-table-item-center" v-on:click="selectItem">x</td>
					<td class="vue-captcha-table-item" v-on:click="selectItem">c</td>
					<td class="vue-captcha-table-item vue-captcha-table-item-center" v-on:click="selectItem">v</td>
					<td class="vue-captcha-table-item" v-on:click="selectItem">b</td>
					<td class="vue-captcha-table-item vue-captcha-table-item-center" v-on:click="selectItem">n</td>
					<td class="vue-captcha-table-item" v-on:click="selectItem">m</td>
				</tr>
        <tr v-show="mode === 'math'">
					<td class="vue-captcha-table-item" v-on:click="selectItemNum">{{arrayForNum[0]}}</td>
					<td class="vue-captcha-table-item vue-captcha-table-item-center" v-on:click="selectItemNum">{{arrayForNum[1]}}</td>
					<td class="vue-captcha-table-item" v-on:click="selectItemNum">{{arrayForNum[2]}}</td>
					<td class="vue-captcha-table-item vue-captcha-table-item-center" v-on:click="selectItemNum">{{arrayForNum[3]}}</td>
					<td class="vue-captcha-table-item" v-on:click="selectItemNum">{{arrayForNum[4]}}</td>
					<td class="vue-captcha-table-item vue-captcha-table-item-center" v-on:click="selectItemNum">{{arrayForNum[5]}}</td>
					<td class="vue-captcha-table-item" v-on:click="selectItemNum">{{arrayForNum[6]}}</td>
					<td class="vue-captcha-table-item vue-captcha-table-item-center" v-on:click="selectItemNum">{{arrayForNum[7]}}</td>
					<td class="vue-captcha-table-item" v-on:click="selectItemNum">{{arrayForNum[8]}}</td>
					<td class="vue-captcha-table-item vue-captcha-table-item-right" v-on:click="selectItemNum">{{arrayForNum[9]}}</td>
				</tr>
			</table>
		</div>
		<div class="options" v-show="!auth">
			<button type="button" v-on:click="picture" v-bind:style="`color: ${color};`" title="Refresh">
				<i class="fa fa-refresh"></i>
			</button>
			<button type="button" v-on:click="opc = (opc === 1) ? 0 : 1"
        v-bind:style="`color: ${color};`" v-show="resolve === 'text' || resolve === 'all'" title="Written">
				<i class="fa fa-pencil"></i>
			</button>
			<button type="button" v-on:click="ContentFixed"
        v-bind:style="`color: ${color};`" v-show="resolve === 'digit' || resolve === 'all'" title="Digit">
				<i class="fa fa-keyboard-o"></i>
			</button>
		</div>
  </div>
</template>

<script>
	'use strict';

	import uuid from 'uuid'
	import 'font-awesome/css/font-awesome.css'
	
  export default {
    name: 'Vuecaptcha',
		props: {
			callSuccess: {
				type: Function,
      	required: true
			},
			color: {
				type: String,
      	required: false,
				default: '#1D9D74'
			},
      mode: {
        type: String,
        required: false,
        default: 'text'   // (default) 'text' -> alphanumeric | 'math' -> operations math
      },
      resolve: {
        type: String,
        required: false,
        default: 'all'    // (default) 'all' -> written and digit | 'text' -> only written | 'digit' -> only digit
      }
		},
		data () {
			return { 
				key: '',
				auth: false,
				opc: 0,
				text: '',
				contenTextTop: 200,
				contenTextLeft: 200,
				errorSelect: 0,
				success: 0,
        preSuccess: false,
        arrayForNum: []
			}
		},
		mounted () {
      if ( (this.mode === 'text' || this.mode === 'math') ) {
        if ( (this.resolve === 'all' || this.resolve === 'text' || this.resolve === 'digit') ) {
    			this.picture()
        } else {
          console.error('[Vue-Captcha] Error: option resolve = \'all\' Or \'text\' Or \'digit\', Not valid \''+this.resolve+'\'.')
        }
      } else {
        console.error('[Vue-Captcha] Error: option mode = \'text\' Or \'math\'.')
      }
		},
		watch: {
			errorSelect (error) {
				if (error > 0) {
					// console.error('[Vue-captcha] Try Errors: ', error)
				}
			},
			success (acert) {
				if (acert === 6) {
					this.callSuccess()
				}
			}
		},
		methods: {
			getKey () {
				let newKey = null

        if (this.mode === 'text') {
  				do {
	  				newKey = uuid()
		  			newKey = newKey.replace('-', '')
			  		newKey = newKey.substr(5, 6)
          } while( this.codex(newKey) )
          this.key = newKey
        } else if (this.mode === 'math') {
          newKey = this.operation()
          this.key = eval( newKey )
        }

				this.opc = 0
        return newKey
			},
			picture () {
				const image = this.$el.children[0].children[0]

				let ctx = image.getContext("2d")
				ctx.clearRect(0, 0, image.width, image.height)
				ctx.font = "25px Arial"

				ctx.strokeStyle = this.color;

				ctx.moveTo(0, 5);
				ctx.lineTo(150, 5);
				ctx.stroke();

				ctx.moveTo(0, 12.5);
				ctx.lineTo(150, 12.5);
				ctx.stroke();

				ctx.moveTo(0, 20);
				ctx.lineTo(150, 20);
				ctx.stroke();

        let left = (this.mode === 'text') ? 35 : 32
				ctx.fillText(this.getKey(), left, 22)
			},
			inputText () {
        let text = (this.mode === 'math') ? Number.parseInt( this.text ) : this.text
				if (this.key === text) {
					this.auth = true
					this.success = 6
				}
			},
			ContentFixed () {
        let el = this.$el
        let _x = 0
        let _y = 0

        /*** position of component for show keyboard ***/
        while( el && !isNaN( el.offsetLeft ) && !isNaN( el.offsetTop ) ) {
          _x += el.offsetLeft - el.scrollLeft;
          _y += el.offsetTop - el.scrollTop;
          el = el.offsetParent;
        }

        this.contenTextTop = _y + 10
        this.contenTextLeft = _x + 210

				this.opc = (this.opc === 2) ? 0 : 2
			},
			selectItem (e) {
				if (this.mode === 'math') return

        let value = e.target.innerText
				if (e.target.className.indexOf(' red') === -1) {
					if (e.target.className.indexOf(' blue') === -1) {
						if (this.key.indexOf(value) === -1) {
							this.errorSelect += 1
							e.target.className += ' red'
						} else {
							this.success += 1
							e.target.className += ' blue'
						}
					} else {
						e.target.className = e.target.className.replace(' blue', '')
						this.success--
					}
				} else {
					e.target.className = e.target.className.replace(' red', '')
					this.errorSelect--
				}
	
				this.auth = (this.success === 6 && this.errorSelect === 0)
			},
      selectItemNum (e) {
        if (this.mode === 'text') return

        let value = e.target.innerText
        let key = String(this.key)

        if (value !== key) {
          if (e.target.className.indexOf(' red') === -1) {
            e.target.className += ' red'
            this.errorSelect++
          } else {
            e.target.className = e.target.className.replace(' red','')
            this.errorSelect--
          }
        }
        if ( (value === key || this.preSuccess)  && this.errorSelect === 0) {
          this.auth = true
					this.success = 6
        } else if (value === key) {
          this.preSuccess = true
          e.target.className += ' blue'
        }
      },
			codex (key) {
				let no = false
				for (let x=0; x<key.length; x++) {
					let count = -1
					for (let y=0; y<key.length; y++) {
						if (key[x] === key[y]) {
							count++
						}
					}
					if (count > 0) {
						no = true
						break
					}
				}
				return no
			},
      operation () {
        let max = 20
        let a = Math.floor((Math.random() * max) + 10)
        let b = Math.floor((Math.random() * max) + 10)
        let o = Math.floor((Math.random() * 9) + 0)
        let cadena = `${a} + ${b}`
        let result = eval( cadena )

        /*** CONTROL ARRAY FOR RANDOM SELECT  ***/
        do {
          let pre = Math.floor((Math.random() * max) + 10) 
          if (pre !== result) {
            this.arrayForNum.push( pre )
          }
        } while(this.arrayForNum.length < 10)
        this.arrayForNum[o] = result
        /***   ***/

        return cadena
      }
		}
  }
</script>

<style scoped>
	.vue-captcha {
		width: 180px;
		text-align: center;
		padding: 5px;
	}
  .vue-captcha-img {
    border: 1px solid #D3D3D3;
  }
	.options button {
		width: 45px;
		height: 20px;
		cursor: pointer;
		background-color: #FFF;
		border: 1px solid;
		margin: 2px;
		outline: transparent;
	}
	.options button:focus, .options button:active {
		box-shadow: 0 0 0 2px #FFF, 0 0 0 3px #1D9D74;
	}
	div.content-text {
		padding: 5px;
	}
  div.content-text > input {
    width: 100%;
    min-width: 100%;
    max-width: 100%;
    height: 25px;
    min-height: 25px;
    max-height: 25px;
    font-size: 13.33px;
  }
	.content-ok {
		width: 150px;
    border-color: #e0f1e9;
    color: #f3faf8;
		margin-left: 10px;
		font-family: proxima-nova, 'Helvetica Neue', Helvetica, Arial, sans-serif;
	}
	.vue-captcha-btn {
		padding: 1px 6px 1px 6px;
	}
	.vue-captcha-table {
		border-collapse: collapse;
	}
	.vue-captcha-table-item {
		padding: 5px;
		padding-left: 8px;
		padding-right: 8px;
		cursor: pointer;
		font-family: proxima-nova, 'Helvetica Neue', Helvetica, Arial, sans-serif;
		border-bottom: 1px solid #1D9D74;
	}
	.vue-captcha-table-item-center {
		border-left: 1px solid #1D9D74;
		border-right: 1px solid #1D9D74;
	}
	.vue-captcha-table-item-right {
		border-left: 1px solid #1D9D74;
	}
	.content-fixed {
		position: fixed;
		border: 0px solid #1D9D74;
		background-color: lightgrey;
	}
	.red {
		background-color: #c7254e;
	}
	.blue {
		background-color: #488dd8;
	}
</style>
