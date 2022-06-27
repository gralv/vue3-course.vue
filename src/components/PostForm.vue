<template>
    <form @submit.prevent>
        <h4>Создать пост</h4>
        <my-input
            v-model="post.title"
            v-focus
            name="title"
            placeholder="название"
        />
        <my-input
            v-model="post.body"
            class="input"
            name="body"
            placeholder="описание"
        />
        <my-button class="btn btn-save" v-on:click="createPost">save</my-button>
    </form>
</template>

<script>
export default {
    data() {
        return {
            post: {
                title: "",
                body: "",
            },
        };
    },
    methods: {
        createPost() {
            this.post.id = Date.now();
            this.$emit("create", this.post);
            this.post = {
                title: "",
                body: "",
            };
        },
    },
};
</script>

<style scoped>
form {
    display: flex;
    flex-direction: column;
}
</style>