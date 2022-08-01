<template>
    <div>
        <section class="add_post cntr_text">
            <h4>New post:</h4>
            <input-text-ui 
                v-model="post.title"
                type="text" 
                placeholder="Title" />
            <input-text-ui
                v-model="post.body"
                type="text" 
                placeholder="Body" />
            <btn-ui @click="createPost" class="btn primary_bg">Create</btn-ui>

        </section>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                post: {
                    title: '',
                    body: '',
                }
            }
        },
        methods: {
            createPost() {
                this.post.id = Date.now();
                this.$emit('create', this.post, 'New post successfully added!')
                this.post = {
                    title: '',
                    body: ''
                }
            },
        }
    }
</script>

<style scoped>

.add_post{
    display: flex;
    flex-direction: column;
    width: 450px;
    margin: 0 auto;
}
</style>