<template>
    <h3>Tasks</h3>
    <p>Click on task to edit the details</p>
    <ul id="list" class="list">
        <li v-for="task in tasks" :key="task.id" :class="task.completed ? 'completed' : 'incomplete'"
            @click.self="editTask(task)">
                {{ task.description }} <span>End on {{ task.Due_date }}</span> <span><input type="checkbox" name=""
                    v-model="task.completed"></span>

            <button class="delete-btn" @click.self="deleteTask(task.id)">x</button>
            
            <div v-if="task.expand" @click.self="task.expand = false">
                <h3>Edit task transaction</h3>
                <form id="form" @submit.prevent="onSubmit">
                    <div class="form-control">
                        <label for="description">Task desctipion</label>
                        <input type="text" id="text" v-model="description" placeholder="Task description..." />
                    </div>
                    <div class="form-control">
                        <label for="dueDate">Due date</label>
                        <input type="datetime-local" name="date" v-model="dateOne" id="">
                    </div>
                    <button class="btn" @click="updateTaskList(task)">Update task</button>
                </form>
            </div>
        </li>
    </ul>
</template>

<script setup>
import { ref, defineProps } from 'vue';
import fecha from 'fecha'
import { useToast } from 'vue-toastification';

const emit = defineEmits(['taskDeleted', 'taskEdited'])
const description = ref([''])
const dateOne = ref([''])
const toast = useToast()

const props = defineProps({
    tasks: {
        type: Array,
        required: true
    }
})

//DELETE TASK

const deleteTask = (id) => {
    emit('taskDeleted', id)
    toast.error('Task deleted')
}


//EDIT TASK

const editTask = (task) => {
    console.log(task)
    task.expand = true
    dateOne.value = task.Due_date
    description.value = task.description 


}

const updateTaskList = (task) => {
    const taskData = {
        id: task.id,
        description: description.value,
        Due_date: fecha.format(new Date(dateOne.value), 'dddd MMMM Do, YYYY HH:mm'),
        Added_date: task.Added_date

    }

    console.log(task)
    task.expand = false
    emit('taskEdited', taskData)
}
//console.log(props.tasks)

</script>

<style></style>