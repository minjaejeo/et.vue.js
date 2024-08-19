<template>
    <div>
        <h1>News Feed</h1>
        <NewsCategory @newsFetched="updateNews" />
        <ul v-if="articles.length">
            <li style="list-style: none;" v-for="(article, index) in articles" :key="index">
                {{ article.title }}
            </li>
        </ul>
        <p v-else>피드가 없습니다.</p>
    </div>
</template>

<script>
import NewsCategory from './NewsCategory.vue';

export default {
    components: {
        NewsCategory,
    },
    data() {
        return {
            articles: [],
        };
    },
    created() {

    },
    methods: {
        updateNews(fetchedArticles) {
            this.articles = fetchedArticles.articles;
        }
    }
};
</script>