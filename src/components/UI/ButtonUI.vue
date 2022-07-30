<template>
    <button>
        <slot></slot>
    </button>
</template>

<script>
    export default {
        name: 'btn-ui'
    }
</script>

<style scoped>
.btn{
    font-weight: 600;
    border: none;
    padding: 3px 15px;
    border-radius: 5px;
    width: fit-content;
    cursor: pointer;
}
.primary_bg{
    color: #fff;
    background: rgb(93, 115, 216);
}
.danger_bg{
    color: #fff;
    background: rgb(182, 5, 50);
}
.success_bg{
    color: #fff;
    background: rgb(5 182 141);
}
.post_actions__btn{
    width: 80px;
    margin: 3px auto;
}
</style>