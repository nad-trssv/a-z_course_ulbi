<template>
    <section class="postList">
        <div class="posts" v-if="posts.length">
            <post-item 
                v-for="post in posts"
                :key="post.id"
                :post="post" 
                @remove="$emit('remove', post)" />
        </div>
        <h3 v-else class="txt_cntr">List is empty</h3>
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