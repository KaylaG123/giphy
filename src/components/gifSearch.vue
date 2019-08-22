<template>
    <div>
        <button>GIF</button>
        <div>

            <div v-if="chosenGIF">
                <img :src="chosenGIF.images.fixed_height.url" />
            </div>

            <div>
                <form @submit.prevent="doSearch">
                    <input v-model="query" type="text" placeholder="GIF Search" class="form-control" />
                    <button type="submit" class="btn btn-primary">Go</button>

                </form>
            </div>
            <div class="results">
                <div v-show="showResults">
                    <result
                        @chooseGIFEvent="chooseGIFHandler(index)"
                        v-for="(result, index) in results"
                        :image="result.images.fixed_height.url"/>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import result from './result.vue'

export default {
    components: { result },
    data() {
        return {
            apiKey: 'WH63Tg4St89UzA55FBLc5RO6aZVRrRFC',
            query: '',
            results: [],
            chosenGIF: null,
            showResults: false
        }
    },

    methods: {
        doSearch() {
            axios.get('https://api.giphy.com/v1/gifs/search?api_key=' + this.apiKey + '&q=' + this.query)
                .then( (response) => {
                    this.results = response.data.data;
                    this.showResults = true;
                })
        },
        chooseGIFHandler(target) {
            this.chosenGIF = this.results[target];
            this.showResults = false;
        }
    }
}

</script>

<style>
    .list-group-item {
        position: relative;
        top: 30px;
        left: 30px;
        overflow: scroll;
    }

    img {
        display: flex;
        justify-content: space-around;
        width: 300px;
        margin: 10px;
        position: relative;

    }

</style>
