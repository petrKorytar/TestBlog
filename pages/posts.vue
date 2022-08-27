<template>
    <div>
        <div class="container">

            <header class="blog-header lh-1 py-3">
                <div class="row flex-nowrap justify-content-between align-items-center">
                    <div class="col-4 pt-1">
                        <a class="link-secondary" href="#">Subscribe</a>
                    </div>
                    <div class="col-4 text-center">
                        <a class="blog-header-logo text-dark" href="#">Můj Blog</a>
                    </div>
                    <div class="col-4 d-flex justify-content-end align-items-center">
                        <a class="link-secondary" href="#" aria-label="Search">
                        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" class="mx-3" role="img" viewBox="0 0 24 24"><title>Search</title><circle cx="10.5" cy="10.5" r="7.5"/><path d="M21 21l-5.2-5.2"/></svg>
                        </a>
                        <a class="btn btn-sm btn-outline-secondary" href="#">Sign up</a>
                    </div>
                </div>
            </header>
        </div>

        <main class="container">
            <div class="p-4 p-md-5 mb-4 rounded text-bg-dark">
                <div class="col-md-6 px-0">
                    <h1 class="display-4 fst-italic">Nadpis</h1>
                    <p class="lead my-3">Vyplňující text Vyplňující text Vyplňující text Vyplňující text.....</p>
                    <p class="lead mb-0"><a href="#" class="text-white fw-bold">Continue reading...</a></p>
                </div>
            </div>
   
        <div class="row g-5">
            <div class="col-md-8">
                <h3 class="pb-4 mb-4 fst-italic border-bottom">
                    Seznam článků
                </h3>
                <div>
                    <div v-for="(article,index) in articles" :key="index">
                        <article class="blog-post">
                            <h2 class="blog-post-title mb-1">{{article.title}}</h2>
                            <p class="blog-post-meta">{{article.createdAt.slice(0,10)}}<a href="#">Jacob</a></p>
                            <p>{{article.content.slice(0,250)}} ....... <NuxtLink :to="`/onePost/${article.slug}`">Continue reading</NuxtLink></p>
                            
                           <!-- <img :src="`${article.image}`" alt="Image" class="rounded"> -->
                           <img src="../assets/obrazek.jpg" alt="Image" class="rounded w-75">
                            <hr>
                        </article>
                    </div>
                </div>
                <nav class="blog-pagination" aria-label="Pagination">
                    <a class="btn btn-outline-primary rounded-pill" href="#">Older</a>
                    <a class="btn btn-outline-secondary rounded-pill disabled">Newer</a>
                </nav>
            </div>

            <div class="col-md-4">
            <div class="position-sticky" style="top: 2rem;">
                <div class="p-4 mb-3 bg-light rounded">
                <h4 class="fst-italic">O mě</h4>
                <p class="mb-0">Customize this section to tell your visitors a little bit about your publication, writers, content, or something else entirely. Totally up to you.</p>
                </div>

                <div class="p-4">
                <h4 class="fst-italic">Archiv</h4>
                <ol class="list-unstyled mb-0">
                    <li><a href="#">March 2021</a></li>
                    <li><a href="#">February 2021</a></li>
                    <li><a href="#">January 2021</a></li>
                    <li><a href="#">December 2020</a></li>
                    <li><a href="#">November 2020</a></li>
                    <li><a href="#">October 2020</a></li>
                    <li><a href="#">September 2020</a></li>
                    <li><a href="#">August 2020</a></li>
                    <li><a href="#">July 2020</a></li>
                    <li><a href="#">June 2020</a></li>
                    <li><a href="#">May 2020</a></li>
                    <li><a href="#">April 2020</a></li>
                </ol>
                </div>

                <div class="p-4">
                <h4 class="fst-italic">Elsewhere</h4>
                <ol class="list-unstyled">
                    <li><a href="#">GitHub</a></li>
                    <li><a href="#">Twitter</a></li>
                    <li><a href="#">Facebook</a></li>
                </ol>
                </div>
            </div>
            </div>
        </div>
        </main>

        <footer class="blog-footer">
        <p>Blog template built for <a href="https://getbootstrap.com/">Bootstrap</a> by <a href="https://twitter.com/mdo">@mdo</a>.</p>
        <p>
            <a href="#">Back to top</a>
        </p>
        </footer>
    </div>
</template>

<script>
   import axios from 'axios';
   export default {
    name:'PostsPage',

    data() {
        return {
            articles:[],
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
        },
    },
   }
</script>

<style>
    @import '../assets/blog.css';
    @import '../assets/blog.rtl.css';
    @import '../assets/bootstrap.min.css';
</style>