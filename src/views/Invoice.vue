<template>
    <div>
        <pre>
            {{text}}
        </pre>
    </div>
</template>

<script>
export default {
    data(){
        return{
            text : ''
        }
    },
    created(){
        this.text = this.$route.params.data
        console.log(this.text);
    }
}
</script>

<style>
</style>