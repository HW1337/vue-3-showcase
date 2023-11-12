<template>
    <div class="app">
        <h1>Посты</h1>
        <my-button @click="showDialog">Создать пост</my-button>
        <my-dialog v-model:show="dialogVisible">
            <post-form @create="createPost"/>
        </my-dialog>
            <post-list :posts="posts" @remove="removePost"/>
        
    </div>
</template>
<script>
import PostForm from "@/components/PostForm"
import PostList from "@/components/PostList"
export default {
    components: {
        PostList, PostForm
    },
    data () {
        return {
            posts: [
                {id: 1, title: "Javascript 1", body: "Описание"},
                {id: 2, title: "Javascript 2", body: "Описание"},
                {id: 3, title: "Javascript 3", body: "Описание"},
            ],
            dialogVisible: false,
        }
    },
    methods: {
        createPost (post) {
            this.posts.push(post);
        },
        removePost(post) {
            this.posts = this.posts.filter(p => p.id !== post.id)
        },
        showDialog() {
            this.dialogVisible = true;
        }
    }
}
</script>
<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}


.app {
    padding: 20px;
}

</style>