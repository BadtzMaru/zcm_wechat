<template>
	<image :class="type" :src="src" mode="widthFix" :style="getStyle"></image>
</template>

<script>
export default {
	props: {
		src: {
			type: String,
			default: ''
		},
		type: {
			type: String,
			default: 'rounded'
		},
		size: {
			type: [String, Number],
			default: 90
		}
	},
	computed: {
		getStyle() {
			return `width: ${this.size}rpx;height: ${this.size}rpx;`;
		}
	},
};
</script>

<style></style>
