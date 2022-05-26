<template>
    <div class="container-fluid">
        <h2 class="text-center py-3 text-uppercase fw-bold">Lista dei post</h2>
        <div class="row p-4">
            <Post v-for="(post, index) in postsList" :key="index" :post="post" />
            <div class="col-12 d-flex justify-content-center">
            <nav aria-label="page-naivgation">
                <ul class="pagination pagination-md">
                    <li class="page-item">
                        <a class="page-link" v-if="currentPage > 1" @click="getPostList(currentPage - 1)" >Previous</a>
                    </li>
                    <li class="page-item">
                        <a class="page-link" >{{ currentPage }}</a>
                    </li>
                    <li class="page-item">
                        <a class="page-link" v-if="currentPage < lastPage" @click="getPostList(currentPage + 1)" >Next</a>
                    </li>
                </ul>
            </nav>
            </div>
        </div>
    </div>
</template>

<script>
import Post from "../components/Post.vue";
export default {
    name: "PostsList",
    components:{
        Post,
    },
    data: function(){
        return {
            postsList: [],
            currentPage : 0,
            lastPage : 0,
        }
    },
    methods:{
        getPostList(page){
            axios.get("http://127.0.0.1:8000/api/posts?page=" + page)
            .then((result) => {
                this.postsList = (result.data.data);
                const { current_page, last_page } = result.data;
                this.currentPage = current_page;
                this.lastPage = last_page;
            })
            .catch((error) => {
                console.warn(error);
            })
        }
    },
    created(){
        this.getPostList(1);
    }
}
</script>

<style>

</style>