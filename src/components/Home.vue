<template>
  <div class="home">
        <div class="title">
            <h1>Ready to start a Quiz?</h1>
        </div>
        <button @click="started" class="start-button">Let's begin!</button>    
    </div>
</template>

<script>
export default {
    emits:['started'],
    methods:{
        started(){
            this.$emit('started');
        }
    }
}
</script>
