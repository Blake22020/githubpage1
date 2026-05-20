<script>
export default {
    data() {
        return {
            draft: '',
            priority: 'md',
        }
    },
    methods: {
        add() {
            if (this.draft.trim() === '') return
            this.$emit('add-task', { title: this.draft.trim(), priority: this.priority })
            this.draft = ''
        },
    },
}
</script>

<template>
    <div class="input-group mb-3">
        <input
            type="text"
            class="form-control"
            placeholder="Новая задача"
            v-model="draft"
            @keydown.enter="add">
        <select class="form-select" style="max-width: 130px;" v-model="priority">
            <option value="hi">Высокий</option>
            <option value="md">Средний</option>
            <option value="lo">Низкий</option>
        </select>
        <button class="btn btn-primary" @click="add">Добавить</button>
    </div>
</template>
