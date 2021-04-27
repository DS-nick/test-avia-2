<template>
    <button class="button">{{ label }}</button>
</template>
<script>
export default {
    props: {
        label: {
            type: String
        }
    }
    
}
</script>
<style scoped>
.button {
    padding: 0.5em 0.8em;
    border: none;
    color: #fff;
    font-size: 1.125em;
    font-weight: 700;
    background-color: #55BB06;
    border-radius: 0.25em;
    width: 100%;
}
</style>