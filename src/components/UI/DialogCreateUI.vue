<template>
    <div class="modal" v-if="show" @click.stop="closeModal">
        <div @click.stop class="modal_content">
            <slot></slot>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'dialog-create-ui',
        props: {
            show: {
                type: Boolean,
                default: false,
            }
        },
        methods: {
            closeModal() {
                this.$emit('update:show', false)
            }
        }
    }
</script>

<style scoped>
.modal{
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
    background: rgba(0,0,0, 0.7);
    position: fixed;   
    display: flex; 
}
.modal_content{
    margin: auto;
    background: #fff;
    border-radius: 12px;
    min-height: 50px;
    min-width: 300px;
    padding: 20px;
}
</style>