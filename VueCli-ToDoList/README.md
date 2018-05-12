# Vue-cli 版本的 Todo-list

#### main.js 部分

```
import Vue from 'vue'
import todolist from './todolist'

Vue.config.productionTip = false

/* eslint-disable no-new */
new Vue({
  el: '#app',
  components: { todolist },
  template: '<todolist/>'
})

```

#### todolist 部分

```
<template>
	<div>
	  <div>
			<input type="text" v-model="inputValue" @keyup.enter="handleSubmit"/>
			<button @click="handleSubmit">提交</button>
	  </div>
	  <ul>
	  	<todo-item 
	  		v-for="(item,index) of list" 
	  		:content="item" 
	  		:index="index" 
	  		:key="index" 
	  		@deleteone="handleDelete">
	  	</todo-item>
	  </ul>
	</div>
</template>

<script>
	import todoitem from './components/todoitem'
	
	export default {
		components: {
			'todo-item' : todoitem
		},
		data () {
			return {
				inputValue: '',
				list: []
			}
		},
		methods: {
			handleSubmit () {
				this.list.push(this.inputValue)
				this.inputValue = ''
			},
			handleDelete (index) {
				this.list.splice(index,1)
			}
		}
	}
</script>

<style>

</style>

```
#### components/todoitem.vue 部分

```
<template>
	<li class="item" @click="handleDelete">{{content}}</li>
</template>

<script>
export default {
	props: ['content','index'],
	methods: {
		handleDelete: function() {
			this.$emit('deleteone',this.index)
		}
	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.item{
	color: green;
}
</style>

```
### 在打包时遇到的页面空白问题：
> config/index.js 这个文件中将build.assetsPublicPath改为 './'