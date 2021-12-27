<template>
    <div class="screen">
        <h1>✨Congratulation 🎉</h1>
        <p>{{Math.round(timer/1000)}} seconds</p>
        <button @click="onStartAgain">Play again</button>
    </div>
</template>

<script>
export default{
    props:{
        timer:{
            type: Number,
            required: true,

        }
    },
    methods:{
        onStartAgain(){
            this.$emit("onStartAgain");
        }
    }
}
</script>