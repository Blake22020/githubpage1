<script>
import TaskInput from './components/TaskInput.vue'
import TaskList from './components/TaskList.vue'

export default {
    components: { TaskInput, TaskList },
    data() {
        return {
            tasks: [
                { title: 'Прочитать главу из книги', priority: 'lo', done: false },
                { title: 'Отправить отчёт по проекту', priority: 'hi', done: false },
                { title: 'Созвониться с Аней', priority: 'md', done: false },
                { title: 'Купить кофе', priority: 'lo', done: true },
            ],
            filter: 'all',
        }
    },
    computed: {
        filteredTasks() {
            if (this.filter === 'all') return this.tasks
            if (this.filter === 'active') return this.tasks.filter(t => !t.done)
            if (this.filter === 'done') return this.tasks.filter(t => t.done)
            return this.tasks
        },
    },
    methods: {
        addTask(task) {
            this.tasks.push({ title: task.title, priority: task.priority, done: false })
        },
        toggleTask(task) { task.done = !task.done },
        removeTask(task) {
            const i = this.tasks.indexOf(task)
            if (i !== -1) this.tasks.splice(i, 1)
        },
    },
}
</script>

<template>
    <div class="container py-4" style="max-width: 600px;">
        <h1 class="h4 mb-3 border-bottom pb-2">Список задач</h1>
        <div class="card">
            <div class="card-body">
                <task-input @add-task="addTask"></task-input>

                <div class="btn-group btn-group-sm mb-3" role="group">
                    <button type="button"
                        class="btn"
                        :class="filter === 'all' ? 'btn-primary' : 'btn-outline-primary'"
                        @click="filter = 'all'">Все</button>
                    <button type="button"
                        class="btn"
                        :class="filter === 'active' ? 'btn-primary' : 'btn-outline-primary'"
                        @click="filter = 'active'">Активные</button>
                    <button type="button"
                        class="btn"
                        :class="filter === 'done' ? 'btn-primary' : 'btn-outline-primary'"
                        @click="filter = 'done'">Готовые</button>
                </div>

                <task-list :tasks="filteredTasks" @toggle="toggleTask" @remove="removeTask"></task-list>
            </div>
            <div class="card-footer text-muted small">
                Всего: {{ tasks.length }} · Готово: {{ tasks.filter(t => t.done).length }}
            </div>
        </div>
    </div>
</template>
