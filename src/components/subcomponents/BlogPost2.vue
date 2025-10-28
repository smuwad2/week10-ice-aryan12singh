<template>
    <!-- TODO: add your template code here Use boostrap card --> 
    <div class="card" style="width: 18rem;">
        <img class="card-img-top" :src="imgLoc" alt="Card image cap">
        <div class="card-body">
            <h5 class="card-title">{{ subject }}</h5>
            <p class="card-text">{{ entry }}</p>
            <!-- slot for actions (e.g., Delete button) -->
            <div class="mt-2">
                <slot></slot>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        // Add code if/as necessary
        // Hint: Add properties subject, entry and mood
        props: {
            subject: { type: String, default: '' },
            entry: { type: String, default: '' },
            mood: { type: String, default: '' }
        },
        computed: {
            imgLoc() {
                const m = (this.mood || 'default').toString().toLowerCase();
                return `/assets/${m}.png`;
            }
        }
    }
</script>

