<template>
    <div class="tvshow">
        <img class="poster" :src="getPoster()" alt="">
        <div class="details">
            <h3>{{tvshow.name}}</h3>
            <ul>
                <li><span class="tvshow-info">Title:</span> {{tvshow.original_name}}</li>
                <li v-if="tvshow.original_language === 'en'"><span class="tvshow-info">Language:</span> <img src="../assets/flag-united-kingdom.png" alt=""></li>
                <li v-else-if="tvshow.original_language === 'it'"><span class="tvshow-info">Language:</span> <img src="../assets/flag-italy.png" alt=""></li>
                <li v-else><span class="tvshow-info">Foreing Language</span> <img src="../assets/white-flag.png" alt=""></li>
                <li><span class="movie-info">Note:</span><i class="fas fa-star" v-for="i in getScore()" :key="'star'+i"></i><i class="far fa-star ciccio" v-for="i in getEmptyStar()" :key="'emptystar'+i"></i></li>
            </ul>
            <p v-if="tvshow.overview.length > 0">{{tvshow.overview.slice(0, 300)}}...</p>
            <p v-else>Nessuna descrizione disponibile.</p>
        </div>
    </div>
</template>

<script>
export default {
    name: 'TvShow',
    props: {
        tvshow: Object
    },
    data() {
        return {
            posterPlaceholder: require("../assets/placeholder.png")
        }
    },
    methods: {
        getPoster() {
            if (this.tvshow.poster_path === null) {
                return this.posterPlaceholder
            } else {
                return 'https://image.tmdb.org/t/p/original' + this.tvshow.poster_path
            }
        },
        getScore() {
            return Math.round(this.tvshow.vote_average / 2)
        },
        getEmptyStar() {
            return 5 - Math.round(this.tvshow.vote_average / 2)
        }
    }
}
</script>

<style lang="scss" scoped>
    .tvshow {
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
        .poster {
            width: 100%;
            height: 100%;
            object-fit: cover;
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
            .tvshow-info {
                color: blue;
                font-weight: bolder;
            }
            
        }
    }
</style>