<template>
  <div class="todo pa-0">
    <v-text-field outlined
    label="Add Task"
    class="pa-3"
    hide-details=""
    clearable
    append-icon="mdi-plus"
    v-model="newTaskTitle"
    @click:append="addTask"
    @keyup.enter = "addTask"/>

    <v-list flat class = "pt-0">
      <div v-for="task in tasks" :key="task.id">
        <v-list-item
          @click="doTask(task.id)" 
          :class="{'blue lighten-5' : task.done}">
          <template>
            <v-list-item-action>
              <v-checkbox :input-value="task.done"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title 
              :class="{'text-decoration-line-through' : task.done}">
                {{task.title}}
              </v-list-item-title>
            </v-list-item-content>

            <v-list-item-action>
              <v-btn icon @click.stop="deleteTask(task.id)">
                <v-icon color = "primary">mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>  
          </template>
        </v-list-item>
        <v-divider></v-divider>
      </div>
    </v-list>
  </div>
</template>

<script>

export default {
  name: 'TodoView',
  data() {
    return{
      tasks: [
      {
        id: 1,
        title: 'Acordar',
        done: true
      },
            {
        id: 2,
        title: 'Comprar bananas',
        done: false
      },
            {
        id: 3,
        title: 'Comer bananas',
        done: false
      },
            {
        id: 4,
        title: 'Almoçar',
        done: true
      },
      ],

      newTaskTitle: "",
    }
  },

  methods: {
    doTask(id){
      let task = this.tasks.filter(task => task.id == id)[0]
      task.done = !task.done
    },
    
    deleteTask(id){
      this.tasks = this.tasks.filter(task => task.id !== id)
  },

  addTask(){
    let newTask ={
      id: Date.now(),
      title: this.newTaskTitle,
      done: false
    }

    this.tasks.push(newTask)
    this.newTaskTitle = ""
  }
}
}
</script>
