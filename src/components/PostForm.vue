<template>
    <form @submit.prevent>
            <h4>Создание поста</h4>
            <input v-bind:value="title" @input="title = $event.target.value" class="input" type="text" placeholder="Название"> 
            <input v-bind:value="body" @input="body = $event.target.value" class="input" type="text" placeholder="Описание">
            <button class="btn" >Создать пост</button>
        </form>
</template>

<script>
    export default {
        
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