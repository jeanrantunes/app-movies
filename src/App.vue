<template>
	<v-app>
		<v-toolbar app>
			<v-toolbar-title class="headline text-uppercase">
				<span>Movies</span>
			</v-toolbar-title>
		</v-toolbar>
		<v-content>
			<ListMovies/>
		</v-content>
	</v-app>
</template>

<script>
import ListMovies from "./components/ListMovies.vue";

export default {
  name: "App",
  components: {
    ListMovies
  }
};
</script>
