<template>
    <div v-if="posts.length > 0">
        <h3>Post</h3>
        <transition-group name="user-list">
            <post-item
                v-for="post in posts"
                :post="post"
                :key="post.id"
                v-on:remove="$emit('remove', post)"
            />
        </transition-group>
    </div>
    <h3 v-else style="color: red">Список пуст</h3>
</template>

<script>
import PostItem from "@/components/PostItem";
export default {
    components: { PostItem },
    props: {
        posts: {
            type: Array,
            required: true,
        },
    },
};
</script>

<style scoped>
.user-list-item {
    display: inline-block;
    margin-right: 10px;
}
.user-list-enter-active,
.user-list-leave-active {
    transition: all 0.25s ease;
}
.user-list-enter-from,
.user-list-leave-to {
    opacity: 0;
    transform: scaleX(0.5);
    /*transform:translate(20px, 30px);*/
}
.user-list-move {
    transition: transform 0.8s ease;
}
</style>
