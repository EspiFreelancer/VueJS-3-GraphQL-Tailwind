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
import { inject, ref, watchEffect } from "vue";
import { useRoute } from 'vue-router';

export default {

name: 'Episodes',

	setup() {
		let episodes = ref([]);
		const info = inject("info");
		const route = useRoute();

		watchEffect(() => {
			fetchGQL(
				"https://rickandmortyapi.com/graphql",
				`query($page: Int) {
					episodes(page: $page) {
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
				`,{
					page: parseInt(route.params.page),
				}
				).then((data) => {
					episodes.value = data.episodes.results;
					info.value = data.episodes.info;
				});
			})

			return {
				episodes,
			};
	},
};
</script>

<style lang="scss" scoped>
</style>