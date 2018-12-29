<template>
    <div id="app">
        <carousel>
            <carousel-slide v-for="n in slides" :index="n-1">
                <div style="position: absolute; left: 0; right:0; text-align: center; top: 50%; color: #FFF; font-size: 16px"></div>
                <img :src="'https://picsum.photos/630/300/?image=' + n" width="100%">
            </carousel-slide>
        </carousel>
        <button @click="addSlide" class="button">Ajouter un slide</button>
        <button @click="removeSlide">Supprimer un slide</button>

    </div>
</template>

<script>
    import Carousel from './components/carousel/Carousel'
    import CarouselSlide from './components/carousel/CarouselSlide'

    export default {
        name: 'App',
        components: { Carousel, CarouselSlide },
        data(){
            return {
                slides: 5
            }
        },
        methods: {
            addSlide(){
                this.slides++
            },
            removeSlide(){
                this.slides--
            }
        }
    }
</script>

<style>

</style>
