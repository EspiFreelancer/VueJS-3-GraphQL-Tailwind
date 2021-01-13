<template>
	<h1>Characters</h1>
	<ul>
		<li v-for="character in characters" :key="character.id">
			<img :src="character.image" :alt="character.name" />
			{{ character.name }}
		</li>
	</ul>
</template>

<script>
import { useQuery } from "../composables/useQuery.js";

export default {

	name: 'characters',

	setup() {
		const { results } = useQuery(
			`query($page: Int) {
				data: characters(page: $page) {
					info {
						count
						pages
						next
						prev
					}
					results {
						id
						name
						image
					}
				}
			}
			`);

		return {
			characters: results,
		};
	},

}
</script>

<style lang="css" scoped>
</style>