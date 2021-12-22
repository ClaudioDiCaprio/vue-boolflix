<template>
    <div class="movie">
        <img class="poster" :src="getPoster()" alt="">
        <div class="details">
            <h3>{{movie.title}}</h3>
            <ul>
                <li><span class="movie-info">Title:</span> {{movie.original_title}}</li>
                <li v-if="movie.original_language === 'en'"><span class="movie-info">Language:</span> <img src="../assets/flag-united-kingdom.png" :alt="info.original_language"></li>
                <li v-else-if="movie.original_language === 'it'"><span class="movie-info">Language:</span> <img src="../assets/flag-italy.png" :alt="info.original_language"></li>
                <li v-else><span class="movie-info">Foreing Languages</span> <img src="../assets/white-flag.png" alt="white_flag"></li>
                <li><span class="movie-info">Note:</span><i class="fas fa-star" v-for="i in getScore()" :key="'star'+i"></i><i class="far fa-star ciccio" v-for="i in getEmptyStar()" :key="'emptystar'+i"></i></li>
            </ul>
            <p v-if="movie.overview.length > 0">{{movie.overview.slice(0, 300)}}...</p>
            <p v-else>No description avaiable.</p>
            
        </div>
    </div>
</template>

<script>
export default {
    name: 'Movie',
    props: {
        movie: Object
    },
    data() {
        return {
            posterPlaceholder: require("../assets/placeholder.png")
        }
    },
    methods: {
        getPoster() {
            if (this.movie.poster_path === null) {
                return this.posterPlaceholder
            } else {
                return 'https://image.tmdb.org/t/p/original' + this.movie.poster_path
            }
        },
        getScore() {
            return Math.round(this.movie.vote_average / 2)
        },
        getEmptyStar() {
            return 5 - Math.round(this.movie.vote_average / 2)
        }
    }
}
</script>

<style lang="scss" scoped>
    .movie {
        background-color: rgba($color: #ffffff, $alpha: .1);
        display: inline-block;
        color: white;
        margin-left: 50px;
        margin: top 50px; 
        margin-bottom: 100px;
        width: calc(15% - 20px);
        min-height: 100%;
        max-height: 480px;
        position: relative;
        // padding: 50px;
        .poster {
            width: 100%;
            height: 100%;
            object-fit: cover;
            // margin: 20px;
        }
        &:hover .details {
            display: block;
        }
        .details {
            padding: 30px;
            background: rgba($color: #000000, $alpha: .9);
            position: absolute;
            top: 0;
            left: 0;
            bottom: 0;
            right: 0;
            display: none;
            h3 {
                margin-bottom: 20px;
            }
            ul {
                margin-bottom: 20px;
                li {
                    list-style: none;
                    font-weight: normal;
                    margin-top: 10px;
                    font-size: .9rem;
                    width: 80%;
                    img {
                        height: 1.2rem;
                    }
                }
            }
            &::after {
                content: '';
                flex: auto;
            }
            .movie-info {
                color: #e50914;
                font-weight: bolder;
            }
            .fa-star{
                color: gold;
            }
            .ciccio{
                color: white;
            }
        }
    }
</style>