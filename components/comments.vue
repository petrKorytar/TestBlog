<template>
    <div>
        <h3 class="pb-4 mb-4 fst-italic border-bottom">Komentáře:</h3>
        <div v-for="(comment,index) in comments" :key="index">
            <article class="blog-post">
                <img :src="`${comment.avatar}`" alt="Avatar" class="rounded">
                <p class="font-weight-bold mb-1">{{comment.name}}</p>
                <p>{{new Date(comment.createdAt).toLocaleString('cz',{
                      month:'numeric',
                      day:'numeric',
                      year:'numeric',})
                  }}</p>
                <p>{{comment.comment}}</p>
                <hr>
            </article>
        </div>
    </div>
</template>

<script>
    import axios from 'axios';

    export default {
        name:"postsComments",

        data() {
            return {
                comments:[],
            }
        },

        async fetch(){
            await this.getComments()
        },

        methods: {
        // Select all comments and push them to the array.
           async getComments(){
                const data = axios.get('https://62fe137ba85c52ee482f275b.mockapi.io/api/v1/comments')
                const result = await data

                result.data.forEach(comment => {
                this.comments.push(comment)})
                console.log(this.comments)
            }
        },
    }
</script>
