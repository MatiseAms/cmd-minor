<template>
	<main>
		<section class="search-giphy">
			<div class="row center">
				<h1>Gifffffs</h1>
			</div>
			<form class="row center search-giphy__form" @submit.prevent="searchGiphy">
				<input
					v-model="giphyQuery"
					type="text"
					placeholder="Search here..."
					class="background--black column small-23 medium-21 large-14 search-giphy__input"
				>
			</form>
			<div class="row center search-giphy__image-grid">
				<div v-for="(item, index) in giphys" :key="index" class="column small-full medium-10 large-4 search-giphy__image-container">
					<img
						v-if="item"
						:src="item.image"
						:alt="item.alt"
						class="search-giphy__image"
					>
				</div>
				<p v-if="!giphys.length">
					0 resultaten, paniek alles in de fik
				</p>
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
			this.giphys = new Array(25);
			const query = this.giphyQuery;
			const APIKey = 'Z9BAE6N7AeyNHU8JzsvcOH3NTNHPL5TM';

			const response = await this.$axios.get(`https://api.giphy.com/v1/gifs/search?q=${query}&api_key=${APIKey}`);
			if (response && response.status === 200) {
				this.giphys = response.data.data.map((item) => {
					return {
						image: item.images.fixed_height.url,
						alt: item.title
					};
				});
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
	&__image-container {
		position: relative;
		background: url('/images/noise.gif');
		margin: grid(0.5);
		height: grid(4);
		transition: 1s ease-out;
		overflow: hidden;
		transform: translateY(0);
		@media #{$medium-down} {
			height: grid(10);
		}
		@media #{$small-only} {
			height: grid(24);
		}
	}
	&__image {
		width: 100%;
		height: 100%;
		object-fit: cover;
	}
}
</style>
