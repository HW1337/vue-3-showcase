<template>
    <div class="app">
        <post-form/>
        <post-list/>
        
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


.app {
    padding: 20px;
}

</style>