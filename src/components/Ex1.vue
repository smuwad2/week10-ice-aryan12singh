<script>
    //import component
    import SoundIcon from './subcomponents/SoundIcon.vue'

    const emojis = (SoundIcon && typeof SoundIcon.data === 'function')
        ? SoundIcon.data().soundEmojis
        : ['🔇','🔈','🔉','🔊']
    
    export default { 
        components: { SoundIcon },
        data() {
            return {
                soundLevel: 0,
                soundEmojis: emojis
            }
        }
    }
</script>

<template>

    Sound level
    <input type="number" min="0" max="3" v-model.number="soundLevel"> 
    <!-- TODO: Add Code Here to make use of the component -->
    <sound-icon :level="soundLevel"></sound-icon>
</template>
