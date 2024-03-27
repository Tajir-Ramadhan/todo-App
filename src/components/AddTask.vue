<template>
    <div>
        <h3>Add new transaction</h3>
        <form id="form" @submit.prevent="onSubmit">
            <div class="form-control">
                <label for="description">Task desctipion</label>
                <input type="text" id="text" v-model="description" placeholder="Task description..." />
            </div>
            <div class="form-control">
                <label for="dueDate">Due date</label>
                <input type="datetime-local" name="date" v-model="dateOne" id="">
            </div>
            <button class="btn">Add task</button>
        </form>

    </div>

</template>

<script setup>

import fecha from 'fecha'
import { ref, defineProps } from 'vue';



const format = ref(['dddd MMMM Do, YYYY HH:mm'])
const dateOne = ref([''])
const date = ref([''])
const description = ref([''])


const registeredDate = fecha.format(new Date(), 'dddd MMMM Do, YYYY HH:mm')
checkDataToEdit()

const props = defineProps({
    dataToEdit: {
        type: Object,
        required: false
    }
})


const emit = defineEmits('taskAdded')


const onSubmit = () => {
    date.value = fecha.format(new Date(dateOne.value), 'dddd MMMM Do, YYYY HH:mm')

    const taskData = {
        taskDescription: description.value,
        dateAdded: registeredDate,
        dueDate: date.value,
        completed: false
    }

    emit('taskAdded', taskData)
    dateOne.value = ''
    description.value = ''


}

</script>

<style lang="scss"></style>