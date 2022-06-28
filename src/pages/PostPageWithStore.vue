<template>
    <div>
        <!--        <h1>{{ $store.getters.doubleLikes }}</h1>-->
        <!--        <div>-->
        <!--            <my-button class="btn" @click="$store.commit('incrementLikes')"-->
        <!--                >Likes</my-button-->
        <!--            >-->
        <!--        </div>-->
        <!--        <div>-->
        <!--            <my-button class="btn" @click="$store.commit('decrementLikes')"-->
        <!--                >Dislikes</my-button-->
        <!--            >-->
        <!--        </div>-->
        <h1>Страница с постами</h1>
        <my-input v-focus
                  :model-value="searchQuery"
                  @update:model-value="setSearchQuery"
                  placeholder="Поиск..."/>
        <div class="app__btns">
            <my-button class="btn"
                       v-on:click="showDialog">Create
            </my-button>
            <my-select v-bind:options="sortOptions"
                       @update:model-value="setSelectedSort"
                       :model-value="selectedSort"/>
        </div>
        <my-dialog v-model:show="dialogVisible">
            <post-form @create="createPost"/>
        </my-dialog>
        <post-list v-if="!isPostsLoading"
                   v-bind:posts="sortedAndSearchedPosts"
                   v-on:remove="removePost"/>
        <div v-else>Идет загрузка...</div>
        <div v-if="posts.length"
             v-intersection="loadMorePosts"
             class="observer"></div>
        <div class="page__wrapper">
            <div
                v-for="pageNumber in totalPages"
                :key="pageNumber"
                class="page"
                v-bind:class="{
                    'current-page': page === pageNumber,
                }"
                v-on:click="changePage(pageNumber)"
            >
                {{ pageNumber }}
            </div>
        </div>
    </div>
</template>

<script>
import PostForm from '@/components/PostForm';
import PostList from '@/components/PostList';
import axios from 'axios';
import {mapState, mapActions, mapGetters, mapMutations} from 'vuex';
import MyButton from '@/components/UI/MyButton';

export default {
    components: {
        MyButton,
        PostList,
        PostForm,
    },
    data() {
        return {
            dialogVisible: false,
        };
    },
    computed: {
        ...mapState({
            posts: (state) => state.post.posts,
            // modificatorValue: '',
            isPostsLoading: (state) => state.post.isPostsLoading,
            selectedSort: (state) => state.post.selectedSort,
            searchQuery: (state) => state.post.searchQuery,
            page: (state) => state.post.page,
            limit: (state) => state.post.limit,
            totalPages: (state) => state.post.totalPages,
            sortOptions: state => state.post.sortOptions,
        }),
        ...mapGetters({
            sortedPosts: 'post/sortedPosts',
            sortedAndSearchedPosts: 'post/sortedAndSearchedPosts',
        }),
    },
    methods: {
        ...mapActions({
            fetchPosts: 'post/fetchPosts',
            loadMorePosts: 'post/loadMorePosts',
        }),
        ...mapMutations({
            setPage: 'post/setPage',
            setSearchQuery: 'post/setSearchQuery',
            setSelectedSort: 'post/setSelectedSort',
        }),
        createPost(post) {
            this.posts.push(post);
            this.dialogVisible = false;
        },
        removePost(post) {
            this.posts = this.posts.filter((p) => p.id !== post.id);
        },
        showDialog() {
            this.dialogVisible = true;
        },
        // changePage(pageNumber){
        //     this.page = pageNumber;
        // },
    },
    mounted() {
        this.fetchPosts();
        //console.log(this.$refs.observer);
        // const options = {
        //     rootMargin: '0px',
        //     threshold: 1.0
        // };
        // const callback = (entries, observer)=>{
        //     if(entries[0].isIntersecting && this.page<this.totalPages){
        //         this.loadMorePosts();
        //     }
        // };
        // const observer = new IntersectionObserver(callback, options);
        // observer.observe(this.$refs.observer);
    },
    watch: {
        // page(){
        //     this.fetchPosts()
        // }
    },
};
</script>

<style>
.app__btns {
    display: flex;
    justify-content: space-between;
}

.page__wrapper {
    display: flex;
    margin-top: 15px;
}

.page {
    border: 1px solid black;
    padding: 10px;
}

.current-page {
    border: 3px solid teal;
}

.observer {
    height: 30px;
    background: green;
}
</style>