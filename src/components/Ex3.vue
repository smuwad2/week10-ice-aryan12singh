<script>
    // Import BlogPost component
    import blogPost from './subcomponents/BlogPost2.vue'
    import axios from 'axios'

    export default {
        components: {
            blogPost
        },
        data() {
            return {
                posts: [] // array of post objects
            }  
        },
        computed: {
            baseUrl() {
                if (window.location.hostname == 'localhost')
                    return 'http://localhost:3000'
                else {
                    const codespace_host = window.location.hostname.replace('5173', '3000')
                    return `https://${codespace_host}`;
                }
            }
        },
        created() { // created is a hook that executes as soon as Vue instance is created
            axios.get(`${this.baseUrl}/posts`)
            .then(response => {
                // this gets the data, which is an array
                this.posts = response.data
                console.log(response.data)
            })
            .catch(error => {
                this.posts = [{ entry: 'There was an error: ' + error.message }]
            })
        },
        methods: {
            deletePost(id) {
                // Optimistically remove the post so UI updates immediately
                this.posts = this.posts.filter(p => p.id != id);

                // Notify backend and refresh to reconcile with server state
                axios.get(`${this.baseUrl}/deletePost`, { params: { id } })
                    .then(() => {
                        return axios.get(`${this.baseUrl}/posts`);
                    })
                    .then(response => {
                        this.posts = response.data;
                    })
                    .catch(error => {
                        console.error('Delete failed', error);
                        // attempt to recover by refetching posts
                        axios.get(`${this.baseUrl}/posts`)
                            .then(r => { this.posts = r.data; })
                            .catch(() => {});
                    });
            }
        }
    }
</script>

<template>
   <!-- TODO: make use of the 'blog-post' component to display the blog posts -->
   <div>
     <blog-post v-for="post in posts" :subject="post.subject" :entry="post.entry" 
       :mood="post.mood" :key="post.id">
         <button class="btn btn-danger" @click="deletePost(post.id)">Delete</button>
     </blog-post>
   </div>
</template>

