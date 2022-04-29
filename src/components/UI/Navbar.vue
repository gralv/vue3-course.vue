<template>
    <div class="navbar">
        <div v-on:click="$router.push('/')">Vue 3</div>
        <div class="navbar__btns">
            <my-button v-on:click="$router.push('/posts')" class="btn">Посты</my-button>
            <my-button v-on:click="$router.push('/about')" class="btn" style="margin-left: 20px">О сайте</my-button>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Navbar",
    }
</script>

<style scoped>
.navbar{
    height: 50px;
    background-color: lightgray;
    box-shadow: 2px 2px 4px gray;
    display: flex;
    align-items: center;
    padding: 0 15px;
}
    .navbar__btns{
        margin-left: auto;
    }
</style>