<template>
    <div>
        <h3>{{ title }}</h3>
        <ul>
        <li v-for="(task, index) in taskList" 
            :key="index">
            {{task.name}} - {{ task.done ? 'Completed' : 'Pending'}}
            <button v-if="!task.done" type="button" @click="toggleTasks(task)">Complete</button>
        </li>
        </ul>
    </div>
</template>

<script>
export default {
    props: {
        title: {
            type: String,
            required: true
        },
        taskList: {
            type: Array,
            required: true
        }
    },
    methods: {
        toggleTasks(task){
            this.$emit('complete', task)
        }
    }
}
</script>
