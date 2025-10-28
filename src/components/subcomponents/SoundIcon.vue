<script>
export default {
    props: {
        level: {
            type: Number,
            default: 0
        }
    },
    data() {
        return {
            soundEmojis: ['🔇','🔈','🔉','🔊']
        }
    }
}
</script>

<template>
    <span>{{ soundEmojis[level] }}</span>
</template>