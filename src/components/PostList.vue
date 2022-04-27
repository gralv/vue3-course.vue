<template>
    <div>
    <h3>Post</h3>
    <post-item
               v-for="post in posts"
               :post="post"
               :key = "post.id"
               v-on:remove="$emit('remove', post)"
    />
    </div>
</template>

<script>
    import PostItem from "@/components/PostItem"
    export default {
        components: {PostItem},
        props:{
            posts:{
                type: Array,
                required: true,
            }
        }
    }
</script>

<style scoped>

</style>