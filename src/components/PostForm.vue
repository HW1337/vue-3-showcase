<template>
    <form @submit.prevent>
            <h4>Создание поста</h4>
            <input v-model="post.title" class="input" type="text" placeholder="Название"> 
            <input v-model="post.body" class="input" type="text" placeholder="Описание">
            <button class="btn" @click="createPost" >Создать пост</button>
        </form>
</template>

<script>
    export default {
        data() {
            return {
                post:{
                    title: '',
                    body: ''
                }
            }
        },
        methods: {
            createPost(){
                this.post.id= Date.mow();
                this.posts.push(newPost);
                this.title="";
                this.body="";         
            }
        }
    }
</script>

<style scoped>
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
form {
    display: flex;
    flex-direction: column;
}
</style>