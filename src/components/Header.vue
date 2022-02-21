<template>
    <div class="header">
        <p class="headerText">
            Cчет-фактура (ПКМ №489)
        </p>
    </div>
</template>

<script>
export default {
    name: "Header",

    data: () => ({
    }),
};
</script>
<style scoped>
.header {
    background: white;
    width: 100%;
    margin-bottom: 10px;
    padding: 30px 0 5px 15px;
}
.headerText {
    color: #858585;
    font-weight: 300;
    font-size: 30px;
    line-height: 1.1;
}
</style>