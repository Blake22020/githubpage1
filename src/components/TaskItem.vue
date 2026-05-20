<script>
export default {
    props: {
        task: Object,
    },
    computed: {
        priorityLabel() {
            if (this.task.priority === 'hi') return 'Высокий';
            if (this.task.priority === 'md') return 'Средний';
            return 'Низкий';
        },
        priorityClass() {
            if (this.task.priority === 'hi') return 'bg-danger-subtle text-danger-emphasis';
            if (this.task.priority === 'md') return 'bg-warning-subtle text-warning-emphasis';
            return 'bg-success-subtle text-success-emphasis';
        },
    },
    methods: {
        toggle() { this.$emit('toggle', this.task) },
        remove() { this.$emit('remove', this.task) },
    },
}
</script>

<template>
    <li class="list-group-item d-flex align-items-center gap-2">
        <input type="checkbox" class="form-check-input mt-0" :checked="task.done" @change="toggle">
        <span class="flex-grow-1 task-title" :class="{ done: task.done }">{{ task.title }}</span>
        <span class="badge" :class="priorityClass">{{ priorityLabel }}</span>
        <button class="btn btn-sm btn-outline-secondary" @click="remove">Удалить</button>
    </li>
</template>
