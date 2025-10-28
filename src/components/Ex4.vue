<script>
import TaskTracker from './subcomponents/TaskTracker.vue'

export default {
    components: {
        TaskTracker
    },
    data() {
        return {
            tasks: []
        }
    },
    methods: {
        addTask(task) {
            this.tasks.push({
                id: Date.now(),
                description: task.description,
                deadline: task.deadline
            });
        },
        removeTask(id) {
            this.tasks = this.tasks.filter(t => t.id !== id);
        }
    }
}
</script>

<template>
    <div>
        <task-tracker @add-task="addTask"></task-tracker>
        
        <div class="mt-3">
            <div v-for="task in tasks" :key="task.id" class="card mb-2" style="width: 18rem;">
                <div class="card-body">
                    <p class="card-text">{{ task.description }}</p>
                    <small class="text-muted">Deadline: {{ task.deadline }}</small>
                    <button class="btn btn-success" @click="removeTask(task.id)">Done</button>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
   
</style>
