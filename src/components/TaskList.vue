<script>
import TaskItem from './TaskItem.vue'

export default {
    components: { TaskItem },
    props: {
        tasks: Array,
    },
    methods: {
        onToggle(task) { this.$emit('toggle', task) },
        onRemove(task) { this.$emit('remove', task) },
    },
}
</script>

<template>
    <ul class="list-group list-group-flush">
        <li v-if="tasks.length === 0" class="list-group-item text-center text-muted py-3">Задач нет</li>
        <task-item
            v-for="task in tasks"
            :key="task.title"
            :task="task"
            @toggle="onToggle"
            @remove="onRemove">
        </task-item>
    </ul>
</template>
