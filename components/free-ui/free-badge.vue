<template>
	<text class="bg-danger font-sm text-white rounded-circle free-badge" :class="badgeClass" :style="badgeStyle">{{ value }}</text>
</template>

<script>
export default {
	props: {
		badgeClass: {
			type: String,
			default: '',
		},
		badgeStyle: {
			type: String,
			default: '',
		},
		value: {
			type: [String, Number],
			default: '',
		},
	},
};
</script>

<style scoped>
.free-badge {
	padding-left: 14rpx;
	padding-right: 14rpx;
	padding-bottom: 6rpx;
	padding-top: 6rpx;
}
</style>
