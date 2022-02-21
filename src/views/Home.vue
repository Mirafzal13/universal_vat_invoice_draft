<template>
    <div class="home grey lighten-3">
        <Header />
        <Content />
    </div>
</template>

<script>
import Header from "../components/Header";
import Content from "../components/Content";
    export default {
        name: 'Home',

        components: {
            Header,
            Content,
        },
    }
</script>
<style scoped>
*{
    margin: 0;
    padding: 10px 15px 0 15px;
}
.home{
    width: 100%;
    height: 100%;
}
</style>