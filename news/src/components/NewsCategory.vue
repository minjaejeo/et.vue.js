<template>
    <div>
        <select v-model="selectedCategory" @change="fetchNews">
            <option value="business">Business</option>
            <option value="technology">Technology</option>
            <option value="sports">Sports</option>
        </select>
    </div>
</template>

<script>
import axios from 'axios';
import { API_KEY } from '../config';

export default {
    data() {
        return {
            selectedCategory: 'business',
            data: [],
        };
    },
    methods: {
        async fetchNews() {
            const url = `https://newsapi.org/v2/top-headlines?country=us&category=${this.selectedCategory}&apiKey=${API_KEY}`;
            try {
                const response = await axios.get(url);
                this.data = response.data;
                this.$emit('newsFetched', this.data);
            }catch (error) {
                console.error('Error fetching news:', error);
            }
        }
    },
    created() {
        this.fetchNews();
    }
}

</script>