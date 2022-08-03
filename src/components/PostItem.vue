<template>
    <div class="post">
        <div class="post_data">
            <strong>{{ post.title }}</strong>
            <p>{{ post.body }}</p>
        </div>
        <div class="post_actions">
            <btn-ui 
                class="btn danger_bg post_actions__btn"
                @click="$emit('remove', post)">
                Remove
            </btn-ui>
            <btn-ui class="btn primary_bg post_actions__btn">Edit</btn-ui>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            post: {
                type: Object,
                required: true,
            }
        }
    }
</script>

<style scoped>
.post{
    width: 250px;
    margin: 10px 3px;
    padding: 0.5rem 1.5rem;
    border-radius: 5px;
    border: 2px solid rgb(185, 184, 184);
    display: flex;
    justify-content: space-between;
}
.post_actions{
    display: flex;
    flex-direction: column;
}
</style>