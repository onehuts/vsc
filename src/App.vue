<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:add="addtodo"></TodoInput>
    <TodoList v-bind:propsData="todo"></TodoList>
    <TodoFooter></TodoFooter>
    <!-- 이건 내 하위 컴포넌트로 등록하는거??? -->
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue';
// vue 파일은 순수 자바스크립트 파일이 아니기 때문에 확장자를 명시해줘야한다.
// 나는 from 뒤에 컴포넌트를 이 이름으로 쓰겠어요...

import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';
import TodoFooter from './components/TodoFooter.vue';

export default {

  // 연습
  data(){
    return {
      todo: []
    }
    
  },
  methods: {
    addtodo: function(data){
      this.todo=data
      console.log(data);
    }
  },

  components: {
    TodoHeader,
    // 원래는
    // TodoHeader:TodoHeader
    // 인데 같으면 이렇게만 써줄 수 있으니깐
    TodoInput,
    TodoList,
    TodoFooter
  } // 이건 내 로컬 컴포넌트로 등록하는거
  
} // 객체 형태를 웹으로 내보내는 형태.
</script>

<style>
body {
    text-align: center;
    background-color: #F6F6F8;
}

input {
    border-style: groove;
    width: 200px;
}

button {
    border-style: groove;
}

.shadow {
    box-shadow: 5px 10px 10px rgba(0,0,0, 0.03);
}
</style>
