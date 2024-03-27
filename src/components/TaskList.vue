<template>
    <h3>Tasks</h3>
    <ul id="list" class="list">
        <li v-for="task in tasks" :key="task.id" :class="task.completed ? 'minus' : 'plus'" @click.self="editTask(task)">
            {{ task.description }} <span>End on {{ task.Due_date }}</span> <span><input type="checkbox" name="" v-model="task.completed"></span>

            <button class="delete-btn" @click.self="deleteTask(task.id)">x</button>
        </li>
    </ul>
</template>

<script setup>
import { defineProps } from 'vue';

const emit = defineEmits(['taskDeleted', 'taskEdited'])

const props = defineProps ({
    tasks: {
        type: Array,
        required: true 
    }
})

//DELETE TASK

const deleteTask = (id) => {
    emit('taskDeleted', id)
    console.log('task deleted' + id)
}


//EDIT TASK

const editTask = (task) => {
    emit('taskEdited', task )

}
//console.log(props.tasks)

</script>

<style >

</style>