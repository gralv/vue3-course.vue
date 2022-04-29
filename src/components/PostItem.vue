<template>
    <div class="post">
        <div>
            <div>{{post.id}}</div>
        <div><strong>Название: </strong>{{post.title}}</div>
        <div><strong>Описание: </strong>{{post.body}}</div>
        </div>
        <div class="post__btns">
            <my-button class="btn" v-on:click="$router.push(`/posts/${post.id}`)">Open</my-button>
            <my-button
                    class="btn"
                    v-on:click="$emit('remove', post)"
            >delete</my-button>
        </div>
    </div>
</template>

<script>
    import MyButton from "./UI/MyButton";
    export default {
        components: {MyButton},
        props:{
            post:{
                type: Object,
                required: true,
            }
        }
    }
</script>

<style scoped>
    .post{
        padding: 15px;
        border: 1px solid teal;
        margin-top: 15px;
        display:flex;
        align-items: center;
        justify-content: space-between;
    }
    .post__btns{
        display:flex;
    }
</style>