<template>
    <div class="mt-4 mx-auto w-75">     
        <div class=" px-4 pb-4 pt-2 mb-4 rounded bg-light text-black w-100 mx-auto">
            <h1 class="display-4 fst-italic">{{searchedTitle}}</h1> 
            <div class="px-0">
                <p class="lead my-3">{{searchedContent}}</p>
            </div>
          <!--  <img :src="`${searchedImage}`" alt="Image" class="rounded">  -->
          <img src="../../assets/obrazek.jpg" alt="Image" class="rounded w-50">
        </div>
        <div class="float-right">
            <NuxtLink to="/" class="btn btn-secondary">Zpět</NuxtLink>
        </div>
        <p>
         <span>Vydáno:</span>
                  {{
                    new Date(this.searchedcreatedAt).toLocaleString('cz',{
                      month:'numeric',
                      day:'numeric',
                      year:'numeric',
                    })
                  }}
        </p>
        <posts-comments/>
    </div>
</template>

<script>
    import axios from 'axios';
    import postsComments from "~/components/comments.vue";

    export default {
        name:"selectedPost",
        components:{postsComments},

        data() {
            return {
                slug: this.$route.params,
                articles:[],
                searchedArticle:[],
                searchedcreatedAt:"",
                searchedTitle:"",
                searchedContent:"",
                searchedImage:"",
            }
        },
      
        async fetch() {
            await this.getArticles()        
        },
        
        methods: {
            // Select all articles and push them to the array.
           async getArticles (){
                const data = axios.get('https://62fe137ba85c52ee482f275b.mockapi.io/api/v1/posts')
                const result = await data

                result.data.forEach(article => {
                this.articles.push(article)
                })

                this.getOneArticle(this.slug.selectedPost)
            },
            // Select one article from array by slug.
            getOneArticle(slug){
                this.searchedArticle = this.articles.filter((searched)=>searched.slug == slug)
                
                this.searchedcreatedAt = this.searchedArticle[0].createdAt
                this.searchedTitle = this.searchedArticle[0].title
                this.searchedContent = this.searchedArticle[0].content
                this.searchedImage = this.searchedArticle[0].image
            }
        },     
    }
</script>
