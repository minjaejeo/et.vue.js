<template>
    <div>
        <select v-model="selectedCategory" @change="fetchNews">
            <option value="business">Business</option>
            <option value="technology">Technology</option>
            <option value="science">Science</option>
            <option value="sports">Sports</option>
            <option value="health">Health</option>
            <option value="entertainment">Entertainment</option>
        </select>
    </div>
</template>

<script>
import axios from 'axios';
import { API_KEY } from '../../process.env';

export default {
    props: {
        page: {
            type: Number,
            required: true,
            default: 1,
        }
    },
    data() {
        return {
            selectedCategory: 'business',
            data: [],
        };
    },
    watch: {
        selectedCategory() {
            this.$emit('update:page', 1);
        },
        page() {
            this.fetchNews();
        }
    },
    methods: {
        async fetchNews() {
            const url = `https://newsapi.org/v2/top-headlines?country=us&category=${this.selectedCategory}&page=${this.page}&apiKey=${API_KEY}`;
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