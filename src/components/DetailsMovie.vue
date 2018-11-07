<template>
    <v-dialog v-model="dialog" fullscreen hide-overlay transition="dialog-bottom-transition">
        <v-card>
            <v-toolbar dark fixed color="primary">
                <v-toolbar-title>{{ movie.title }}</v-toolbar-title>
                <v-spacer></v-spacer>
                <v-btn icon dark @click.native="dialog = false">
                    <v-icon>close</v-icon>
                </v-btn>
            </v-toolbar>
            <v-card class="overview-movie" absolute>
                {{movie.overview}}
            </v-card>
            <img v-if="movie.backdrop_path" v-bind:src="'https://image.tmdb.org/t/p/original'+movie.backdrop_path" alt="">
        </v-card>
    </v-dialog>
</template>
<script>
export default {
    name: "DetailsMovie",
    props: ['dialog','movie']
}
</script>
<style>
.v-dialog img {
	width: 100%;
}
.overview-movie {
	position: fixed;
	bottom: 0;
	padding: 20px;
}
</style>

