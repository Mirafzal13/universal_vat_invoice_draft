<template>
    <div>
        <rapi-doc
        spec-url="https://api.faktura.uz/swagger/docs/V1"
        render-style="read"
        style="height: 100vh; width: 100%"
        >
        </rapi-doc>
    </div>
</template>
<script>
import "rapidoc";
export default {
    name: "App",
};
</script>

<style>
* {
    margin: 0;
    padding: 0;
}
</style>