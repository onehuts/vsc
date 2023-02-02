<template>
    <div>
        <input type="text"
               placeholder="할일을 입력하세요!"
               v-model="newTodoItem"
               v-on:keyup.enter="addTodo">
        <span class="addContainer" v-on:click="addTodo">
            <i class="addBtn fa fa-plus" aria-hidden="true"></i>
        </span>
        
    </div>
</template>

<script>
export default {
    data(){
        return{
            newTodoItem: ''
        }
    },
    methods: {
        addTodo(){
            // 현재 입력한 할 일 목록을 저장해야 돼요!
            // 지금 서버에 연결을 할 수 없어요!
            // 서버쪽 데이터베이스에 해당 정보를 저장할 수 없어요!
            // 그래서 browser가 가지고 있는 저장 장소를 이용할거에요!
            // browser내부에 저장장소가 크게 2가지 있어요!
            // Storage와 IndexedDB가 있어요!
            // 그 중 Storage를 사용해 보아요!
            // 다시 Storage는 LocalStorage와 SessionStorage로 나눠져요!
            // 우리는 그 중 가장 일반적인 LocalStorage를 이용할거에요!
            // 우리가 JavaScript를 이용해서 이 저장공간에 내가 원하는 데이터를 저장할 수 있어요!
            // 데이터는 Map형태로 저장이 가능해요!(key, value의 쌍으로)
            // 여러 프로그램에 의해 데이터가 중복되는걸 방지하기 위해
            // 각 데이터는 domain으로 구분되어서 저장됩니다.

            if(this.newTodoItem !== ""){
                localStorage.setItem(this.newTodoItem, this.newTodoItem);
                // 이 키워드 사용하면 이 공간을 내가 이용할 수 있어!
                // localStorage.setItem('키값','변수값')
                
                this.$emit('add',localStorage);
                
                this.newTodoItem="";
            }
        }
    }
}
</script>

<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  font-size: 0.9rem;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #6478fb, #8763fb);
  display: inline-block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color: white;
  vertical-align: middle;
}
</style>