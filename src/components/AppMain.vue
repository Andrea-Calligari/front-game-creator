<template>
    <main class="">
        <div class="container text-center">
            <div class="row ">
                <ul v-for="character in characters" class="col-12 text-light ">
                    <li class="d-flex justify-content-center align-items-center gap-3">
                        Nome carattere: <h4 class="text-light">{{ character.name }}</h4> 

                    </li>
                </ul>
            </div>
            <button @click="setPage(n)" class="btn btn-primary m-4" v-for="n in lastPage">{{ n }}</button>
        </div>
    </main>
</template>

<script>
// import { store } from '../store.js';
// import ElmBtnCount from './ElmBtnCount.vue';
import axios from 'axios';
export default {
    // components: { ElmBtnCount },
    data() {
        return {
            // store,
            characters: [],
            CurrentPage: 1,
            lastPage: null
        }
    },
    methods: {
        fetchData() {
            axios.get('http://127.0.0.1:8000/api/characters', {

                params: {
                    page: this.CurrentPage,
                }

            }).then((res) => {
                console.log(res.data);
                this.characters = res.data.characters.data
                this.lastPage = res.data.characters.last_page
                // console.log(this.lastPage)
            })
        },
        setPage(n) {
            if (n === this.CurrentPage) return

            this.CurrentPage = n;
            this.fetchData();
        }
    },
    mounted() {
        this.fetchData();
    }
}
</script>


<style lang="scss" scoped></style>