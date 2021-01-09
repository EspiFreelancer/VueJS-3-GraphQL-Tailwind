<template>
	<h1>Episodes</h1>
	<ul>
		<li v-for="episode in episodes" :key="episode.id">
			{{ episode.name }}
		</li>
	</ul>
</template>

<script>
import { request as fetchGQL } from "graphql-request"; 
import { ref } from "vue";
export default {

name: 'Episodes',

	setup() {
		let episodes = ref([]);

		fetchGQL(
			"https://rickandmortyapi.com/graphql",
			`query {
				episodes {
					info {
						count
						pages
						next
						prev
					}
					results {
						id
						name
						air_date
						episode
						created
					}
				}
			}
			`
			).then((data) => {
				episodes.value = data.episodes.results;
			});

			return {
				episodes,
			};
	},
};
</script>

<style lang="scss" scoped>
</style>