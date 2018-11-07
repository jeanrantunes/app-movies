<template>
	<div>
		<v-container grid-list-md>
			<h1>Filmes populares</h1>
			<v-btn
				color="pink"
				dark
				v-on:click="showDrawer"
				>
				Meus favoritos
			</v-btn>
			<v-layout row wrap>
				<v-flex v-for="item in movies" v-bind:key="item.index">
					<v-card v-on:click="1">
						<v-img
							v-if="item.backdrop_path"
							v-bind:src="'https://image.tmdb.org/t/p/w780'+item.backdrop_path"
							height="200px"
						>
							<v-container
								fill-height
								fluid
								pa-2
							>
								<v-layout fill-height>
									<v-flex xs12 align-end flexbox>
										<span class="headline white--text">{{ item.title }}</span>
									</v-flex>
								</v-layout>
							</v-container>
						</v-img>

						<v-card-actions>
							<v-spacer></v-spacer>
							<v-btn icon v-on:click="openDialog(item)">
								<v-icon>info</v-icon>
							</v-btn>
							<v-badge left overlap>
								<span slot="badge" v-if="item.like">{{ item.like }}</span>
								<v-btn icon v-on:click="item.like ++">
									<v-icon>favorite</v-icon>
								</v-btn>
							</v-badge>
							<v-btn icon v-on:click="saveMovie(item)">
								<v-icon v-if="item.isFavorite" color="amber">bookmark</v-icon>
								<v-icon v-else>bookmark</v-icon>
							</v-btn>
						</v-card-actions>
					</v-card>
				</v-flex>
			</v-layout>
		</v-container>

		<navigator ref="navigator"></navigator>

		<details-movie v-bind:dialog="dialog" v-bind:movie="movieForDialog"></details-movie>

	</div>
</template>

<script>
import axios from "axios"
import DetailsMovie from './DetailsMovie.vue'
import Navigator from './Navigator.vue'
const requester = axios.create({
	baseURL: "https://api.themoviedb.org/3"
});
export default {
	name: "ListMovies",
	components: {
		DetailsMovie,
		Navigator
	},
	beforeMount() {
		requester
		.get("/movie/popular", {
			params: {
				api_key: "958de68fa51fec79b1311cc75a6400b7",
				language: "pt-BR",
				page: 1
			}
		})
		.then(response => {
			let movies = response.data.results
			movies.forEach(item => {
				item["like"] = 0
				item["isFavorite"] = false
				this.movies.push(item)
			})
		})
	},
	data() {
		return {
			movies: [],
			favorites: [],
			dialog: false,
			movieForDialog: {}
		}
	},
	methods: {
		saveMovie(movie) {
			if(this.favorites.find(item => {
				return item.id == movie.id
			})) {
				return
			}
			this.favorites.push(movie)
			movie.isFavorite = true
		},
		openDialog(movie) {
			this.movieForDialog = movie
			this.dialog = true
		},
		showDrawer() {
			this.$refs.navigator.show(this.favorites)
		}
	}
};
</script>

<style scoped>
.title {
	color: #fff;
	padding: 4px;
}
</style>
