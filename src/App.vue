<template>
    <div class="app">
        <post-form @create="createPost"/>
        <post-list v-bind:posts="posts"
                   v-on:remove="removePost"/>
    </div>
</template>

<script>
    import PostForm from "./components/PostForm";
    import PostList from "./components/PostList";
    export default {
        components:{
            PostList, PostForm
        },
        data() {
            return{
                posts:[
                    {id: 1, title:"Name1", body:"Body1"},
                    {id: 2, title:"Name2", body:"Body2"},
                    {id: 3, title:"Name3", body:"Body3"},
                ],
            }
        },
        methods: {
            createPost(post){
                this.posts.push(post);
            },
            removePost(post){
                this.posts = this.posts.filter(p=>p.id!==post.id)
            }
        }
    }
</script>

<style>
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
.app{
    padding:20px;
}

</style>