<template>
    <div class="dialog" v-if="show" @click.stop="hideDialog">
        <div @click.stop class="dialog__content">
            <slot></slot>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'my-dialog',
        mixins: [toggleMixin],
        mounted() {
            console.log('dialog mounted')
        }
    }
</script>

<style scoped>
.dialog {
    top:0;
    bottom:0;
    right: 0;
    left: 0;
    background: rgba(0,0,0,0.5);
    position: fixed;
    display: flex;
}

.dialog__content {
    border-radius: 12px;
    background: white;
    margin: auto;
    padding: 20px;
}
</style>