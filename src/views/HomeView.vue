<template>
  <div>
    <Header />
    <div class="container">
      <AddTask @taskAdded="handleAdedTask" :dataToEdit />
      <TaskList :tasks="tasks" @taskDeleted="handleTaskDeleted" @taskEdited="handleEditedTask" />


    </div>
  </div>
</template>

<script setup>
// @ is an alias to /src
import { onMounted, ref } from 'vue'
import Header from '../components/Header.vue'
import AddTask from '../components/AddTask.vue'
import TaskList from '../components/TaskList.vue'
import { useToast } from 'vue-toastification'

const dataToEdit = ref([''])
const toast = useToast()

const tasks = ref([])

onMounted (
  () => {
    const savedTasks = JSON.parse(localStorage.getItem('tasks'))

    if(savedTasks){
      tasks.value = savedTasks
    }
  }
)

const handleAdedTask = (taskData) => {
  tasks.value.push({
    id: genRandomId(),
    description: taskData.taskDescription,
    Added_date: taskData.dateAdded,
    Due_date: taskData.dueDate,
    completed: taskData.completed
  })

  saveToLocalStorage()
  toast.success('task added successfuly')

}

//Handle deleted task

const handleTaskDeleted = (id) => {
  tasks.value = tasks.value.filter((task) => task.id !== id)
  saveToLocalStorage()

}


//Handle edited
const handleEditedTask = (taskData) => {

  handleTaskDeleted(taskData.id)

  tasks.value.push({
    id: taskData.id,
    description: taskData.description,
    Added_date: taskData.Added_date,
    Due_date: taskData.Due_date,
    completed: false
  })

  saveToLocalStorage()
  toast.success('Task edited successfuly')
  
}

//generate id
const genRandomId = () => {
  return Math.floor(Math.random() * 100000)
}

//SAVE OT LOCAL STORAGE
const saveToLocalStorage =  () => {
  localStorage.setItem('tasks', JSON.stringify(tasks.value))
}

</script>
