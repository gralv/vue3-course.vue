<template>
    <div>
        <h1>Страница с постами</h1>
        <my-input v-focus v-model="searchQuery" placeholder="Поиск..."/>
        <div class="app__btns">
            <my-button class="btn" v-on:click="showDialog">Create</my-button>
            <my-select v-bind:options="sortOptions" v-model="selectedSort"/>
        </div>
        <!--        <my-dialog v-model:show="dialogVisible">-->
        <!--            <post-form @create="createPost"/>-->
        <!--        </my-dialog>-->
        <post-list
            v-bind:posts="sortedAndSearchedPosts"
            v-if="!isPostsLoading"
        />
        <div v-else>Идет загрузка...</div>
        <!--        <div v-intersection="loadMorePosts" class="observer"></div>-->

    </div>
</template>

<script>
import PostForm from '@/components/PostForm';
import PostList from '@/components/PostList';
import axios from 'axios';
import {ref} from 'vue';
import {usePosts} from '@/hooks/usePosts';
import useSortedPosts from '@/hooks/useSortedPosts';
import useSortedAndSearchedPosts from '@/hooks/useSortedAndSearchedPosts';

export default {
    components: {
        PostList,
        PostForm,
    },
    data() {
        return {
            posts: [],
            dialogVisible: false,
            sortOptions: [
                {value: 'title', name: 'По названию'},
                {value: 'body', name: 'По содержимому'},
            ],
        };
    },
    methods: {},
    setup(props) {
        const {posts, totalPages, isPostsLoading} = usePosts(10);
        const {selectedSort, sortedPosts} = useSortedPosts(posts);
        const {searchQuery, sortedAndSearchedPosts} = useSortedAndSearchedPosts(sortedPosts);
        return {
            posts,
            totalPages,
            isPostsLoading,
            selectedSort,
            searchQuery,
            sortedAndSearchedPosts,
        };
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
