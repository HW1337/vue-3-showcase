<template>
    <div class="app">
        <post-form/>
        <post-list :posts="posts"/>
        
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
        }
    },
    methods: {
        createPost () {

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