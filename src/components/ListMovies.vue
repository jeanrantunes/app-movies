<template>
	<div>
		<v-container>
			<h1>Mais populares</h1>
			<v-layout row wrap>
				<v-flex xs4 v-for="item in movies" v-bind:key="item.index">
					<v-card>
						<v-img
							src="https://cdn.vuetifyjs.com/images/cards/house.jpg"
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
							<v-btn icon>
								<v-icon>favorite</v-icon>
							</v-btn>
							<v-btn icon>
								<v-icon>bookmark</v-icon>
							</v-btn>
						</v-card-actions>
					</v-card>
				</v-flex>
			</v-layout>
			<ol>
				<li v-for="item in movies" v-bind:key="item.index">{{item.title}}</li>
			</ol>
			
		</v-container>
	</div>
</template>

<script>
import axios from "axios";
const requester = axios.create({
  	baseURL: "https://api.themoviedb.org/3"
});
export default {
	name: "ListMovies",
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
			this.movies = response.data.results
		})
		.catch(error => {
			console.log(error)
		})
	},
	data() {
		return {
			movies: []
		}
	}
};
</script>

<style scoped>
ol {
	text-align: left;
}
</style>
