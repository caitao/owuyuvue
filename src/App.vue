<template>
  <div id="app">
    <img src="./assets/wu.png">
    <hello></hello>
    <input
      v-model="newItem"
      v-on:keyup.enter="addNewTodo"
      placeholder="添加一个TODO列表"
    >
    <ul>
      <li
           v-for="item in items"
           v-bind:class="{finished: item.finished}"
           v-on:click="toggleFinish(item)">{{item.label}}</li>
           <!--v-on:remove="todos.splice(index, 1)"   v-bind:title="todo" -->
      <li>{{newItem}}</li>
    </ul>
  </div>
</template>

<script>
import Hello from './components/Hello'
import Store from './store'

export default {
  name: 'app',
  components: {
    Hello
  },
  data: function () {
    return {
      items: Store.fetch(),
      newItem: ''
    }
  },
  watch: {
    items: {
      handler: function (items) {
        Store.save(items)
      },
      deep: true
    }
  },
  methods: {
    toggleFinish: function (item) {
      return (item.finished = !item.finished)
    },
    addNewTodo: function () {
      this.items.push({
        label: this.newItem,
        finished: false
      })
      this.newItem = ''
    }
  }
}
</script>

<style>
.finished {
  font-weight: bold;
}
#app {
  font-family: 'Microsoft YaHei', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
ul {
 margin: 0px auto;
 width: 150px;
 text-align: left;
}
</style>
