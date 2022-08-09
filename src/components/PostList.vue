<template>
    <section class="postList">
        <div class="posts" v-if="posts.length">
        <transition-group name="post-list">
            <post-item 
                v-for="post in posts"
                :key="post.id"
                :post="post" 
                @remove="$emit('remove', post)" />
        </transition-group>
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
.post-list-item {
  display: inline-block;
  margin-right: 10px;
}
.post-list-enter-active,
.post-list-leave-active {
  transition: all 0.4s ease;
}
.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
.post-list-move {
  transition: transform 0.4s ease;
}
</style>