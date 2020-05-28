<template>
  <div class>
    <header class="py-8 md-5">
      <h1 class="block uppercase font-bold text-center tracking-widest">todos</h1>
    </header>
    <div class="max-w-lg mx-auto ">
      <div >
        <div class="flex mb-8">
          <input
            class="appearance-none rounded-lg py-2 px-4 border-2 border-gray-200 w-full text-sm focus:border-gray-300 focus:outline-none"
            type="text"
            placeholder="Please add a todo here .."
            v-model="state.input_task"
          />
          <button
            type="button"
            class="ml-1 border-2 text-center text-white w-20 bg-green-600 rounded-lg focus:outline-none"
            @click="addTodo"
          >
            <p>Add</p>
          </button>
        </div>
        <div>
          <div class="flex items-center mb-6" v-for=" todo in state.list" :key="todo.id">
            <div
              class="w-8 h-8 mr-3 rounded border border-grey inline-flex justify-center items-center bg-green-600"
              @click="updateTodo(todo.id)"
            >
              <svg
                v-show="todo.isCompleted"
                class="w-1/2 fill-current text-white"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 512 512"
              >
                <path
                  d="M504.502,75.496c-9.997-9.998-26.205-9.998-36.204,0L161.594,382.203L43.702,264.311c-9.997-9.998-26.205-9.997-36.204,0
                    c-9.998,9.997-9.998,26.205,0,36.203l135.994,135.992c9.994,9.997,26.214,9.99,36.204,0L504.502,111.7
                    C514.5,101.703,514.499,85.494,504.502,75.496z"
                />
              </svg>
            </div>

            <span class="border-b-2 border-grey-500 w-full tracking-wider">{{todo.task}}</span>
          </div>
        </div>
      </div>
       <div id="footer" >
           Total: {{total_count}} | Todo: {{total_count-completed_count}} | Finished: {{completed_count}}
    </div>
    </div>  
   

  </div>
</template>

<script lang="ts">
import { reactive, computed } from "vue";

interface Todo {
  id:number 
  task:string
  isCompleted: boolean
}

interface State {
  list:Todo[]
  input_task:string
}
export default {
  setup() {
    let state = reactive<State>({
      list: [
        {
          id: 1,
          task: "This is the first task.",
          isCompleted: true
        },
        {
          id: 2,
          task: "This is my second task, haven't finished!",
          isCompleted: false
        }
      ],
      input_task: ""     
     
    });

    let total_count=computed(()=>state.list.length);
    let completed_count=computed(()=>state.list.filter(todo=>todo.isCompleted).length)

    const addTodo = () => {
      console.log("dd");
      let { list, input_task } = state;
      if (input_task.length == 0) return;
      if (list.filter(todo => todo.task === input_task).length > 0) {
        state.input_task = "";
        return;
      }
      const new_id = list.length + 1;
      let new_todo:Todo= {
        id: new_id,
        task: input_task,
        isCompleted: false
      };
      list.push(new_todo);
      //total_count.value+=1;
      state.input_task = "";
    };
    const updateTodo = (id:number)=> {
      const { list } = state;
      state.list = list.map(t =>
        t.id === id ? { ...t, isCompleted: !t.isCompleted } : t
      );
      // completed_count.value=state.list.filter(todo=>todo.isCompleted).length;
    };

    return {
      state,
      addTodo,
      updateTodo,
      total_count,
      completed_count
    };
  }
};
</script>

<style>
</style>