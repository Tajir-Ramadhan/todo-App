<template>
  <div >
    <Header />
    <div class="container">
      <AddTask @taskAdded="handleAdedTask" :dataToEdit />
      <TaskList :tasks="tasks" @taskDeleted="handleTaskDeleted" @taskEdited="handleEditedTask"/>


    </div>
  </div>
</template>

<script setup>
// @ is an alias to /src
import { ref} from 'vue'
import Header from '../components/Header.vue'
import AddTask from '../components/AddTask.vue'
import TaskList from '../components/TaskList.vue'

const dataToEdit = ref([''])

const tasks = ref([
        { id: 1, description: 'Flower', Added_date:400,  Due_date: 237.98, completed: false },
        { id: 2, description: 'Salary', Added_date:400,  Due_date: 300, completed: false },
        { id: 3, description: 'Book', Added_date:400,  Due_date: -10, completed: false },
        { id: 4, description: 'Camera', Added_date:400,  Due_date: 150, completed: false }
])

const handleAdedTask = (taskData) => {
  tasks.value.push({
    id: genRandomId(),
    description: taskData.taskDescription,
    Added_date: taskData.dateAdded,
    Due_date: taskData.dueDate,
    completed: taskData.completed
  })


}

//Handle deleted task

const handleTaskDeleted = (id) => {
        tasks.value = tasks.value.filter( (task) => task.id !== id)

        
    }


//Handle edited
const handleEditedTask = (task) => {
  dataToEdit.value = task
  console.log( dataToEdit.value)
}

//generate id
const genRandomId = () => {
  return Math.floor(Math.random() * 100000)
}

</script>
