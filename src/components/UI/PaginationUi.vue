<template>
    <div class="pagination_wrapper">
        <div 
            class="page" 
            v-for="page in totalPages" 
            :key="page"
            :class="{
                'current_page': pageCurrent === page
            }"
            @click="$emit('change', page)" >
            {{ page }}
        </div>
    </div>
</template>

<script>
    export default {
        name: 'pagination-ui',
        props: {
            totalPages: {
            },
            pageCurrent: {
            }
        },
    }
</script>

<style lang="css" scoped>
.pagination_wrapper{
    display: flex;
    margin-top: 15px;
    flex-wrap: wrap;
}
.page{
    font-size: 12px;
    font-family: cursive;
    padding: 0.2em 0.5em;
    margin: 5px 2px;
    border: 1px solid rgb(93 115 216);
    border-radius: 8px;
    background: rgb(255 255 255);
    color: rgb(93 115 216);
    font-weight: 700;
    cursor: pointer;
}
.page:hover{
    background: rgba(93, 132, 216, 0.616);
    color: #fff;
}
.current_page{
    background: rgb(93, 115, 216);
    color: #fff;
}
</style>