<template>
	<main>
		<giphySearch />
	</main>
</template>

<script>
export default {
	components: {
		giphySearch: () => import('~/components/giphy-search.vue')
	}
};
</script>
