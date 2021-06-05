<template>
    <button class="button" :disabled="disabled" @click="$emit('click')">
        <slot></slot>
    </button>
</template>
<script>
export default {
    name: "VueButton",
    props: {
        disabled: {
            type: Boolean,
            default: false
        }
    }
}
</script>

<style>
.button {
    border: none;
    outline: none;
    background-color: transparent;
    padding: 5px 10px;
    text-align: center;
    font-size: 16px;
    color: #111111;
    border-radius: 5px;
    cursor: pointer;
}
.button-primary {
    background-color: #3e3edd;
    color: #e6e6e6;
}
.button-danger {
    background-color: #f16166;
    color: #e6e6e6;
}
</style>
