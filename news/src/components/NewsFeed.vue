<template>
    <div>
        <h1>News Feed</h1>
        <NewsCategory :page="page" @update:page="page = $event" @newsFetched="updateNews"  />
        <ul v-if="articles.length">
            <li style="list-style: none;" v-for="(article, index) in articles" :key="index">
                {{ article.title }}
            </li>
        </ul>
        <p v-else>피드가 없습니다.</p>
        <div class="pagination">
            <button @click="prevPage" :disabled="page === 1">Previous</button>
            <span>Page {{ page }}</span>
            <button @click="nextPage">Next</button>
        </div>
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
            page: 1,
        };
    },
    methods: {
        // news articles 추출
        updateNews(data) {
            this.articles = data.articles;
        },
        // 이전 페이지
        prevPage() {
            if (this.page > 1) {
                this.page--;
            }
        },
        // 다음 페이지
        nextPage() {
            this.page++;
        }
    }
};
</script>