<template>
  <div>
    <h1>Minha Lista de Tarefas!</h1>
    <button @click="handleShowHideList">
        Ver a Lista
    </button>
    <br>

    <input 
        type="text" 
        @keyup.enter="addTask"
        v-model="state.currentTask" 
        v-focus>

    <ul v-if="state.showList">
        <li
            v-for="(task, index) in state.tasks"
            @dblclick="complete(task)"
            :key="`${task}-${index}`"
            class="task-item"
            :class="{
                'line-through': task.isDone
            }"
        >
            {{ task.name}}
            <button 
                @click="remove(task)"
            >
                &times;
            </button>
        </li>
    </ul>
    <p v-else>Lista de tarefas escondidas!</p>
  </div>
</template>

<script>
import { reactive } from 'vue'

const focus = {
    inserted: (el) => {
        el.focus()
    }
}

export default {
    directives: {
        focus
    },
    setup () {
      const state = reactive({
        currentTask: '',
        showList: false,
        tasks: [
            {name: 'Fazer o curso', isDone: false}
        ]
      })

      function addTask() {
        state.tasks.push({
            name: state.currentTask,
            isDone: false
        })
        state.currentTask = '';
      }
       
      function remove (task) {
        state.tasks = state.tasks.filter(t => t.name !== task.name)
      }
      
      function handleShowHideList () {
        state.showList = !state.showList
      }

      function complete(task) {
        state.tasks = state.tasks.map(t => {
            if (t.name === task.name)  {
                return { ...t, isDone: !t.isDone}
            }
            return {...t}
        })
      }

      return {
        state,
        addTask,
        remove,
        handleShowHideList,
        complete
      }
    }
}
</script>
<style scope>
.line-through {
    text-decoration: line-through;
}
.task-item {
    cursor: pointer;
}
</style>