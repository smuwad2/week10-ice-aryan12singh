<script>
export default {
    data() {
        return {
            description: '',
            deadline: ''
        }
    },
    methods: {
        addTask() {
            if (this.description && this.deadline) {
                this.$emit('add-task', {
                    description: this.description,
                    deadline: this.deadline
                });
                // Clear form
                this.description = '';
                this.deadline = '';
            }
        }
    }
}
</script>

<template>
    <div>
        <div class="mb-3">
            <label for="taskDescription" class="form-label">Task Description</label>
            <input 
                type="text" 
                class="form-control" 
                id="taskDescription" 
                v-model="description"
                placeholder="Enter task description"
            >
        </div>
        <div class="mb-3">
            <label for="taskDeadline" class="form-label">Deadline</label>
            <input 
                type="date" 
                class="form-control" 
                id="taskDeadline" 
                v-model="deadline"
            >
        </div>
        <button class="btn btn-primary" @click="addTask">Add New Task</button>
    </div>
</template>


