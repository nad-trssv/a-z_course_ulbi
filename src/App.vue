<template>
<div>
    Works!
    Some picture...

    <div v-if="newPostStatus">
        <span class="newPost_status">{{ newPostStatus }}</span>
    </div>

    <div>
        likes:
        <button @click="addLike"><strong>{{ likes }}</strong></button>
    </div>
    <div>
        dislikes:
        <button @click="addDislike"><strong>{{ dislikes }}</strong></button>
    </div>
    <post-form
        @create="createPost"/>
    <post-list 
        :posts="posts" />
</div>
</template>

<script>
import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";

export default {
    components: {
        PostList, PostForm
    },
    data() {
        return {
            likes: 0,
            dislikes: 0,
            newPostStatus: '',
            posts: [
                {id:1, title: 'Javascript', body: 'JS Description'},
                {id:2, title: 'Vue', body: 'Vue Description'},
                {id:3, title: 'React', body: 'React Description'}
            ],
        }
    },
    methods: {
        addLike() {
            this.likes += 1;
        },
        addDislike() {
            this.dislikes += 1;
        },
        createPost(post, status) {
            this.posts.push(post);
            this.newPostStatus = status;
        },
    },
}

</script>

<style> 
/* scoped - применимо только данному компоненту */

section{
    margin: 80px 0;
}
.cntr_text{
    text-align: center;
    font-family:'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
}
.newPost_status{
    position: absolute;
    top: 50px;
    right: 50px;
    color: #fff;
    font-weight: 800;
    border-radius: 9px;
    background: rgb(71, 136, 131);
    padding: 5px 10px;
    font-family: monospace;
}
</style>