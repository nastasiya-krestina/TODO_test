<script>
  export default {
    //создание переменных, с которыми взаимодействуем
    data() {
      let count = 0;
      return {
        currentTask: '',
        editValue: '',
        //создание массива задач
        tasks: [
          {
            text: 'Задача 1',
            inCompleted: false,
            isEditing: false
          },
          {
            text: 'Задача 2',
            inCompleted: false,
            isEditing: false
          }
        ]
      }
      
    },

    methods: {
      //добавление задачи в список
      addTask: function () {
        if(this.currentTask === '') {return};
        this.tasks.push({
          text: this.currentTask,
          isCompleted: false,
          isEditing: false
        });
        this.currentTask = '';
      },

      //удаление задачи из списка
      removeTask: function(taskText) {
        this.tasks = this.tasks.filter(task => {
          return task.text != taskText;
        })
      },

      //перевод статуса задачи в режим изменения
      changeEditing: function(taskText) {
        this.editValue = taskText;
        this.tasks = this.tasks.map(task => {
          if(task.text === taskText) {
            task.isEditing = !task.isEditing;
          }
          return task;
        })
      },

      //изменение задачи
      editTask: function (taskText) {
        this.tasks = this.tasks.map(task => {
          if(task.text === taskText) {
            task.isEditing = !task.isEditing;
            task.text = this.editValue;
          }
          return task;
        })
      },
    }
}

</script>

<template>
  <div class="todo__container">
    <h1 class="todo__title">
      Список задач
    </h1>
    <div class="todo__contain">
      <input class="todo__input" type="text" placeholder="Введите задачу" v-model="currentTask" @keyup.enter = "addTask">
      <button class="todo__button" @click="addTask">Добавить</button>
    </div>
    <ul class="todo__list" >
      <li class="todo__task" v-for="task in tasks" >
        <div class="todo__task-contain">
            <input class="todo__check" type="checkbox" @click="task.isCompleted = !task.isCompleted">
            <input class="todo__task-text" type="text" v-if="task.isEditing" @keyup.enter = "editTask(task.text)" v-model = "editValue" >
            <span class="todo__task-text" :class="{'strike': task.isCompleted}" v-else> {{task.text}} </span>
            <button class="todo__button" @click="changeEditing(task.text)">Изменить</button>
            <button class="todo__button" @click="removeTask(task.text)">Удалить</button>
        </div>
      </li>   
    </ul>
    
  </div>
  
</template>

<style scoped>
  .todo__container {
    max-width: 1000px;
    margin: auto;
    font-family: Arial;
  }

  .todo__contain {
    display: flex;
    justify-content: space-between;
    margin-bottom: 15px;
  }

  .todo__title {
    padding-bottom: 15px;
  }

  .todo__input {
    padding: 10px;
    margin-right: 20px;
    width: 100%;
    background: transparent;
    border: 1px solid grey;
    border-radius: 10px;
  }

  .todo__button {
    padding: 10px 20px;
    border-radius: 10px;
    border: none;
    background: #22c1c3;
    font-size: 14px;
    text-alidn: center;
  }

  .todo__button:not(:last-child) {
    margin-right: 5px;
  }

  .todo__button:hover {
    cursor: pointe;
  }

  .todo__task {
    margin-bottom: 10px;
  }

  .todo__task-contain {
    display: flex;
    justify-content: space-between;
    align-items: center;
  } 

  .todo__check {
    margin-right: 15px;
  }

  .todo__task-text {
    width: 100%;
    margin-right: 15px;
  }

  .strike {
    text-decoration: line-through;
  }

</style>
