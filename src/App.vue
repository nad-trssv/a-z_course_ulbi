<template>
<div>
    Works!
    Some picture...

    <div v-if="newPostStatus">
        <span class="newPost_status">{{ newPostStatus }}</span>
    </div>

    <div>
        likes:
        <btn-ui @click="addLike">{{ likes }}</btn-ui>
    </div>
    <div>
        dislikes:
        <btn-ui @click="addDislike">{{ dislikes }}</btn-ui>
    </div>

    <dialog-create-ui v-model:show="modalVisible">
        <post-form
            @create="createPost" 
        />
    </dialog-create-ui>

    <h4 class="cntr_text">List</h4>
    <btn-ui 
        @click="showModal"
        class="btn success_bg">Create new Post +</btn-ui>

    <post-list 
        :posts="posts"
        @remove="removePost" />
</div>
</template>

<script>
import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";
import DialogCreateUi from './components/UI/DialogCreateUI.vue';

export default {
    components: {
    PostList,
    PostForm,
    DialogCreateUi,
},
    data() {
        return {
            likes: 0,
            dislikes: 0,
            newPostStatus: '',
            modalVisible: false,
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
            this.modalVisible = false;
        },
        removePost(post){
            this.posts = this.posts
            .filter(p => p.id !== post.id)
        },
        showModal() {
            this.modalVisible = true
        }
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
.txt_cntr{
    text-align: center;
}
</style>