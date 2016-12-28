<template>
  <div id="app">
    <h1>{{title}}</h1>
    <h2 v-text="title"></h2>
    <h2 v-html="title2"></h2>
    <ul>
      <li v-for="item in items" :class="[liClass,{finished:item.isFinished}]">
        <h4>{{item.label}}</h4>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      title: 'this is a todo list',
      title2: '<em>?</em>this is a todo list',
      items:[
        {
          label:'coding',
          isFinished:false
        },
        {
          label:'walking',
          isFinished:true
        }
      ],
      liClass:"thisisLiClass"
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.finished{
  text-decoration:line-through;
}
.thisisLiClass{color:red;}
</style>
