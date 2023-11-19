<template>
    <div class="app">
        <h1>Посты</h1>
        <my-input 
        v-model="searchPost"
        placeholder="Поиск..."
        />
        <div class="app__btns">
            <my-button
                @click="showDialog">
                Создать пост
            </my-button>
            <my-select 
                v-model="selectedSort" 
                :options="sortOptions"
            />
        </div>
        <my-dialog v-model:show="dialogVisible">
            <post-form @create="createPost"/>
        </my-dialog>
            <post-list :posts="sortedAndSearchedPosts" @remove="removePost" v-if="!isPostsLoading"/>
            <div v-else> Идёт загрузка... </div>
            <div ref="observer" class="observer"> </div>
    </div>
</template>
<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import MyButton from "@/components/UI/MyButton";
import MySelect from "@/components/UI/MySelect";
import axios from 'axios';
import { getCurrentInstance, getTransitionRawChildren } from "vue";
export default {
    components: {
        MySelect, MyButton, PostList, PostForm
    },
    data () {
        return {
            posts: [],
            dialogVisible: false,
            isPostsLoading: false,
            selectedSort: '',
            searchPost: '',
            page: 1,
            limit: 10,
            totalPages: 0,
            sortOptions: [
                {value: 'title', name: 'По названию'},
                {value: 'body', name: 'По содержанию'},
            ]
        }
    },
    methods: {
        createPost (post) {
            this.posts.push(post);
            this.dialogVisible = false;
        },
        removePost(post) {
            this.posts = this.posts.filter(p => p.id !== post.id)
        },
        showDialog() {
            this.dialogVisible = true;
        },
        async fetchPosts() {
            try {
                this.isPostsLoading = true
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
                    params: {
                        _page: this.page,
                        _limit: this.limit
                    }
                } );
                this.totalPages =Math.ceil(response.headers['x-total-count']/this.limit);
                this.posts = response.data;
            } catch (e) {
                alert("Ошибка")
            } finally {
                this.isPostsLoading = false;
            }
        },
        async loadMorePosts() {
            try {
                this.page +=1;
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
                    params: {
                        _page: this.page,
                        _limit: this.limit
                    }
                } );
                this.totalPages =Math.ceil(response.headers['x-total-count']/this.limit);
                this.posts = [...this.posts, ...response.data];
            } catch (e) {
                alert("Ошибка")
            } 
        }
    },
    mounted () {
        this.fetchPosts();
        this.$refs.observer
        const options = {
            rootMargin: "0px",
            threshold: 1.0,
        };
        const callback = (entries, observer) => {
            if(entries[0].isIntersecting && this.page < this.totalPages) {
                this.loadMorePosts()
            };
        };
        const observer = new IntersectionObserver(callback, options);
        observer.observe(this.$refs.observer);
    },
    computed: {
        sortedPosts() {
            return [...this.posts].sort((post1, post2)=> post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
        },
        sortedAndSearchedPosts() {
            return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchPost.toLowerCase()))
        }
    },
    watch: {
       
    }
}
</script>
<style>

.app__btns {
    margin:15px 0;
    display: flex;
    justify-content: space-between;
}
.page__wrapper {
    display: flex;
    margin-top: 15px;
}
.page {
    border: 1px solid black;
    padding: 10px;
}
.current-page {
    border: 2px solid green;
}
.observer {
    height: 0px;
}
</style>