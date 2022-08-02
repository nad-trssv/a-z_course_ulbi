<template>
    <section class="postList">
        <h4 class="cntr_text">List</h4>
        <div class="posts">
            <post-item 
                v-for="post in posts"
                :key="post.id"
                :post="post" 
                @remove="$emit('remove', post)" />
        </div>
    </section>
</template>

<script>
import PostItem from './PostItem.vue'
export default {
  components: { PostItem },
    props: {
        posts: {
            type: Array,
            required: true,
        }
    }
}
</script>

<style scoped>
.posts{
    display: flex;
    flex-wrap: wrap;
}
</style>