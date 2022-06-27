<template>
    <div class="dialog" v-if="show" v-on:click.stop="hideDialog">
        <div v-on:click.stop class="dialog__content">
            <slot></slot>
        </div>
    </div>
</template>

<script>
import toggleMixin from "@/mixins/toggleMixin";
export default {
    name: "my-dialog",
    mixins: [toggleMixin],
};
</script>

<style scoped>
.dialog {
    top: 0px;
    bottom: 0px;
    right: 0px;
    left: 0px;
    background: rgba(0, 0, 0, 0.5);
    position: fixed;
    display: flex;
}
.dialog__content {
    margin: auto;
    background: white;
    border-radius: 12px;
    min-height: 50px;
    min-width: 300px;
    padding: 20px;
}
</style>