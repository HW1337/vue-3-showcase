<template>
    <div>
        <button @click="addLike">Like</button>
        <button @click="addDislike">Dislike</button>
    </div>
    <div>
        <div>Количество лайков <strong>{{ likes }}</strong></div>
        <div>Количество дизлайков <strong>{{ dislikes }}</strong></div>
    </div>
</template>
<script>
export default {
    data () {
        return {
            likes: 0,
            dislikes: 0,
        }
    },
    methods: {
        addLike() {
            this.likes++
        },
        addDislike() {
            this.dislikes++
        }
    }
}
</script>
<style>

</style>