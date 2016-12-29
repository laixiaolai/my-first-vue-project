<template>
  <div id="app">
    <heads></heads>
    <h1>{{title}}</h1>
    <h2 v-text="title"></h2>
    <h2 v-html="title2"></h2>
    <input type="text" v-model="newItem" v-on:keyup.enter="addNew">
    <ul>
      <li v-for="item in items" :class="[liClass,{finished:item.isFinished}]" v-on:click="toggleFinish(item)">
        <h4>{{item.label}}</h4>
      </li>
    </ul>
    <foots></foots>
  </div>
</template>

<script>
import Heads from './components/Header'
import Foots from './components/Footer'
import Store from './store.js'

export default {
  name: 'app',
  data () {
    return {
      title: 'this is a todo list',
      title2: '<em>?</em>this is a todo list',
      items:Store.fetch(),
      liClass:"thisisLiClass",
      newItem:''
    }
  },
  methods:{
    toggleFinish:function(item){
      item.isFinished=!item.isFinished;
    },
    addNew:function(){
      console.log(this.newItem);
      this.items.push({
        label:this.newItem,
        isFinished:false
      });
      this.newItem='';
    }
  },
  watch:{
    items:{
      handler:function(items){
        Store.save(items);
      },
      deep:true
    }
  },
  components:{
    Heads,Foots
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
