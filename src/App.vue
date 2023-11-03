<template>
    <div class="app">
        <form @submit.prevent>
            <h4>Создание поста</h4>
            <input v-bind:value="title" @input="title = $event.target.value" class="input" type="text" placeholder="Название"> 
            <input v-bind:value="body" @input="body = $event.target.value" class="input" type="text" placeholder="Описание">
            <button class="btn" @click="createPost">Создать пост</button>
        </form>
        <div class="post" v-for="post in posts">
            <div><strong>Название:</strong>{{  post.title }}</div>
            <div><strong>Описание:</strong>{{  post.body }}</div>
        </div>
    </div>
</template>
<script>
export default {
    data () {
        return {
            posts: [
                {id: 1, title: "Javascript 1", body: "Описание"},
                {id: 2, title: "Javascript 2", body: "Описание"},
                {id: 3, title: "Javascript 3", body: "Описание"},
            ],
            title: "",
            body: "",
        }
    },
    methods: {
        createPost () {
            const newPost = {
                id: Date.now(),
                title: this.title,
                body: this.body,
            }
            this.posts.push(newPost);
            this.title="";
            this.body="";
        },
    }
}
</script>
<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
.post {
    padding: 15px;
    border: 2px solid green;
    margin-top: 15px;
}
.btn {
    margin-top: 15px;
    align-self: flex-end;
    padding: 10px 15px;
    background: none;
    color: green;
    border: 1px solid green;
}
.input {
    width: 100%;
    border: 1px solid green;
    padding: 10px 15px;
    margin-top: 15px;
}
.app {
    padding: 20px;
}
form {
    display: flex;
    flex-direction: column;
}
</style>