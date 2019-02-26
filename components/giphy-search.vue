<template>
	<section class="search-giphy">
		<div class="row center search-giphy__title">
			<div class="column">
				<h1>Welcome to Giphy</h1>
			</div>
		</div>
		<form class="row center search-giphy__form" @submit.prevent="changeRoute">
			<input
				v-cloak
				v-model="giphyQueryModel"
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
</template>

<script>
export default {
	props: {
		giphyQuery: {
			type: String,
			default: ''
		},
		giphys: {
			type: Array,
			default: () => []
		}
	},
	data() {
		return {
			giphyQueryModel: this.giphyQuery
		};
	},
	methods: {
		changeRoute() {
			const query = this.giphyQueryModel;
			this.$router.push(`/${query}`);
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
