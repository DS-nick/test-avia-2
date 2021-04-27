<template>
    <div class="checkbox">
        <input type="checkbox" name="" class="checkbox-input" :checked="!checked"  :id="id"
                v-on:change="onChange($event, id)"
        >
        <label :for="id" class="checkmark"></label>
    </div>
</template>
<script>
export default {
    props: {
        id: {
            type: String
        }, 
       checked: {
           type: Boolean
       }
    },
    methods: {
        onChange({target}, id) {
            this.$emit('clicked', id, !target.checked)
        }
    }
}
</script>
<style scoped>
.checkbox-input {
    display: none;
}
.checkmark {
    display: inline-block;
    width: 0.75em;
    height: 0.75em;
    background-color: #55BB06;
    border-radius: 2px;
    
    position: relative;
}
.checkmark::after {
    content: "";
    position: absolute;
    right: 0.2em;
    width: 0.23em;
    height: 0.40em;
    border-bottom: 2px solid #fff;
    border-right: 2px solid #fff;
    transform: rotate(45deg);
    
}
.checkbox-input:checked ~ .checkmark {
    background-color: #fff;
    border: 1px solid #B9B9B9;
}
</style>