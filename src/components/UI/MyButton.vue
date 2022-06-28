<template>
    <button>
        <slot></slot>
    </button>
</template>

<script>
export default {
    name: "my-button"
}
</script>

<style scoped>
.btn {
    align-self: flex-end;
    padding: 5px 30px;
    background: none;
    color: teal;
    border: 1px solid teal;
}

.btn-save {
    margin-top: 15px;
}
</style>