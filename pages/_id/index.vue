<template>
	<main>
		<giphySearch :giphys="giphys" :giphy-query="giphyQuery" />
	</main>
</template>

<script>
export default {
	components: {
		giphySearch: () => import('~/components/giphy-search.vue')
	},
	async asyncData({ params, $axios }) {
		const query = params.id;
		const APIKey = 'Z9BAE6N7AeyNHU8JzsvcOH3NTNHPL5TM';

		const response = await $axios.get(`https://api.giphy.com/v1/gifs/search?q=${query}&api_key=${APIKey}`);

		const giphys =
			response && response.status === 200 ? response.data.data.map((item) => item.images.fixed_height.url) : [];

		return {
			giphyQuery: query,
			giphys
		};
	}
};
</script>
