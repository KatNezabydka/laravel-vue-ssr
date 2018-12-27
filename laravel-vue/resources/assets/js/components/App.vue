<template>
    <div>
        <p>It's my first vui application</p>
        {{ message }}
    </div>
</template>
<script>
    export default {
        data() {
            return {
                message: 'Hello World'
            }
        }
    }
</script>
<style scoped>
    div {
        text-align: center;
    }
</style>