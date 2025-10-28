<script>
    //import component
    import SoundIcon from './SoundIcon.vue'
    
    export default { 
        components: { SoundIcon },
        data() {
            return {
                soundLevel: 0
            }
        }
    }
</script>

<template>

    <div style="display:flex; align-items:center; gap:8px;">
    Sound level
    <input type="number" min="0" max="3" v-model.number="soundLevel"> 
    <!-- TODO: Add Code Here to make use of the component -->
    <SoundIcon :level="soundLevel" />
  </div>
</template>

