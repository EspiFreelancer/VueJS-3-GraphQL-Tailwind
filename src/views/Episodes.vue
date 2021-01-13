<template>
	<h1>Episodes</h1>
	<ul>
		<li v-for="episode in episodes" :key="episode.id">
			{{ episode.name }}
		</li>
	</ul>
</template>

<script>
import { useQuery } from "../composables/useQuery.js";

export default {

	name: 'Episodes',

	setup() {
		const { results } = useQuery(
			`query($page: Int) {
				data: episodes(page: $page) {
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
			`);

		return {
			episodes: results,
		};
	},

};
</script>

<style lang="scss" scoped>
</style>