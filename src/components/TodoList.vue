<template>
    <section>
        <ul>
            <li v-for="(todoItem, index) in todoItems" :key="todoItem" class="shadow">
                <!-- index는 삭제할 때 대비 뽑아놓은 것
                     v-for 이용할 때 웬만하면 v-bind로 key값을 잡아줘..
                     browser의 효율적인 랜더링을 위해! -->
        <i class="checkBtn fa fa-check" aria-hidden="true"></i>
        {{ todoItem }}
        <!-- @click은 v-on:click과 동일하게 동작합니다. 
                추가적으로 @click="[method1(), method2()]" 와 같이 사용하면
                클릭이벤트를 여러개 설정할 수 있습니다.
            -->
        <span
            class="removeBtn"
            type="button"
            @click="removeTodo(todoItem, index)"
        >
          <i class="fa fa-trash" aria-hidden="true"></i>
        </span>
      </li>
        </ul>
    </section>
    <!-- 영역잡는 태그 -->
</template>

<script>
export default {
    data(){
        return {
            todoItems: []
        }
    },
    methods:{
        removeTodo(todoItem, index){
            localStorage.removeItem(todoItem);
            // 특정 인덱스에서 부여한 숫자만큼의 인덱스를 삭제합니다.
            this.todoItems.splice(index,1);
        }
    },
    props: {
        propsData: Array
    },
    created: function(){
        // localStorage에서 데이터를 가져다가
        // todoItems에다 넣어요!
        for(let i=0; i<localStorage.length; i++){
            if(localStorage.key(i) !== 'loglevel:webpack-dev-server'){
            this.todoItems.push(localStorage.key(i))
            // key(i) -> 순차적으로 key값을 가져온다.
            }
        }
    },

    watch: {
        propsData: {
            handler: function(){
                this.propsData=localStorage
            }

        }
    }
}
</script>

<style>
ul {
  list-style-type: none;
  padding-left: 0px;
  margin-top: 0;
  text-align: left;
}

li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}

.checkBtn {
  line-height: 45px;
  color: #62acde;
  margin-right: 5px;
}

.removeBtn {
  margin-left: auto;
  color: #de4343;
}
</style>