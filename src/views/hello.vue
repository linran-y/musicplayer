<template>
    <div class="app" @click="sayhello">
        app
        u
    </div>
</template>

<script>
    export default {
        name: "hello",
        data() {
            return {
                food:123123,
                list:[123123,231232]
            }
        },
        methods:
            {
                sayhello(){alert("hello")}
            }
    }
</script>

<style scoped>

</style>