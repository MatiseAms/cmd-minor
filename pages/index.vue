<template>
	<main>
		<section class="search-giphy">
			<div class="row center search-giphy__title">
				<div class="column">
					<h1>Welcome to Giphy</h1>
				</div>
			</div>
			<form v-cloak class="row center search-giphy__form" @submit.prevent="searchGiphy">
				<input
					v-model="giphyQuery"
					autofocus
					type="text"
					placeholder="Search here..."
					class="background--black colum small-20 medium-14 search-giphy__input"
				>
			</form>
			<div class="row center">
				<div v-for="(item, index) in giphys" :key="index" class="column small-full medium-10 large-4 plaatje">
					<img v-if="item" :src="item" alt="We have to provide an alt text but for now we don't have any">
				</div>
			</div>
		</section>
	</main>
</template>

<script>
export default {
	data() {
		return {
			giphyQuery: '',
			giphys: []
		};
	},
	methods: {
		async searchGiphy() {
			const query = this.giphyQuery;
			const APIKey = 'Z9BAE6N7AeyNHU8JzsvcOH3NTNHPL5TM';

			const response = await this.$axios.get(`https://api.giphy.com/v1/gifs/search?q=${query}&api_key=${APIKey}`);

			if (response && response.status === 200) {
				this.giphys = response.data.data.map((item) => item.images.fixed_height.url);
			}
		}
	}
};
</script>

<style lang="scss">
@import '~tools';
.search-giphy {
	margin-top: grid(1);
	&__input {
		font-size: grid(40/60);
		padding: grid(40/60 1);
		border: none;
		margin-top: grid(1);
	}
}
img {
	width: 100%;
	height: 100%;
	object-fit: cover;
}
.plaatje {
	background: hotpink;
	margin: grid(0.5);
	height: grid(4);
	@media #{$medium-down} {
		height: grid(10);
	}
	@media #{$small-only} {
		height: grid(24);
	}
}
</style>
