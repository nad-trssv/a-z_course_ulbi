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

    <div class="posts_pagination_v1">
        <h4 class="cntr_text">Posts</h4>

        <section class="sorting">

            <input-text-ui 
                v-model="searchQuery"  
                placeholder="Search"  
                class="search_fullw"
            />

            <div class="sort_btns">
                <btn-ui 
                    @click="showModal"
                    class="btn success_bg">Create new Post +</btn-ui>
                <sort-ui
                    v-model="selectSort"
                    :options="sortOptions" />

            </div>
        </section>

        <post-list 
            :posts="sortedAndSearchedPosts"
            @remove="removePost"
            v-if="!isLoadingPosts" />
        <loading-ui v-else></loading-ui>

        <div ref="observer" class="observer"> OBSERVER </div>
        <pagination-ui 
            :totalPages="totalPages"
            :pageCurrent="page"
            @change="changePage" />
    </div>

</div>
</template>

<script>
import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";
import axios from 'axios';

export default {
    components: {
    PostList,
    PostForm
},
    data() {
        return {
            likes: 0,
            dislikes: 0,
            newPostStatus: '',
            modalVisible: false,
            posts: [],
            searchQuery: '',
            isLoadingPosts: false,
            selectSort: '',
            page: 0,
            limit: 10,
            totalPages: 0,
            sortOptions: [
                {value: 'title', name: 'By name'},
                {value: 'body', name: 'By description'},
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
        },
        changePage(pageNumber) {
            this.page = pageNumber;
        },
        async fetchPosts() {
            try {
                this.isLoadingPosts = true;
                setTimeout( async() => {
                    const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
                        params: {
                            _page: this.page,
                            _limit: this.limit,
                        }
                    });

                    this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
                    
                    this.posts = response.data;
                }, 1000);
            } catch(e) {
                alert(e);
            } finally {
                this.isLoadingPosts = false;
            }
        },
        async loadMorePosts() {
            try {
                this.page += 1;
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
                    params: {
                        _page: this.page,
                        _limit: this.limit
                    }
                });
                this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
                
                this.posts = [...this.posts, ...response.data];
            } catch(e) {
                alert(e);
            }
        },
    },
    mounted() {
        this.fetchPosts();

        //Obserever API https://developer.mozilla.org/ru/docs/Web/API/Intersection_Observer_API
        // this.$refs.observer - наблюдаемый объект в DOM-элементе
        const options = {
            rootMargin: '0px',
            threshold: 1.0
        }
        const callback = (entries, observer) => {
            // console.log('Пересечён'); - будет выполняться несколько раз,нас это неустраивает, 
            // поэтому мы будем использовать значение isIntersecting ->
            if(entries[0].isIntersecting) {
                this.loadMorePosts();
            }
        };
        const observer = new IntersectionObserver(callback, options);
        observer.observe(this.$refs.observer);
    },
    computed: {
        sortedPosts() {
            return [...this.posts].sort((post1, post2) =>  post1[this.selectSort]?.localeCompare(post2[this.selectSort]))
        },
        sortedAndSearchedPosts() {
            return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
        }
    },
    watch: {
        page() {
            this.fetchPosts();
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
.sort_btns{
    margin: 15px 0;
    display: flex;
    justify-content: space-between;
}
.search_fullw {
    width: -webkit-fill-available;
}
#app{
    margin: 5px 20px;
}
.observer{
    height: 30px;
    background:blue;
    color: #fff;
    text-align: center;
    height: max-content;
    padding: 5px 0;
}
</style>