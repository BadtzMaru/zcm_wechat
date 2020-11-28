<template>
	<div style="z-index:9999;overflow:hidden;" v-if="status">
		<!-- 蒙板 -->
		<div v-if="mask" class="position-fixed top-0 right-0 bottom-0 left-0" :style="getMaskColor" @click="hide"></div>
		<!-- 弹出框内容 -->
		<div class="position-fixed bg-white" :class="getBodyClass" :style="getBodyStyle"><slot></slot></div>
	</div>
</template>

<script>
export default {
	props: {
		// 蒙板颜色是否开启
		maskColor: {
			type: [Boolean],
			default: false,
		},
		// 是否开启蒙板
		mask: {
			type: Boolean,
			default: true,
		},
		// 是否处于底部
		bottom: {
			type: Boolean,
			default: false,
		},
		// 弹出层内容高度
		bodyHeight: {
			type: Number,
			default: 0,
		},
		// 弹出层内容宽度
		bodyWidth: {
			type: Number,
			default: 0,
		},
	},
	data() {
		return {
			status: false,
			x: -1,
			y: -1,
			maxX: 0,
			maxY: 0,
		};
	},
	computed: {
		getMaskColor() {
			let i = this.maskColor ? 0.5 : 0;
			return `background-color: rgba(0,0,0,${i});`;
		},
		getBodyClass() {
			let bottom = this.bottom ? 'left-0 right-0 bottom-0' : 'rounded border';
			return bottom;
		},
		getBodyStyle() {
			let left = this.x > -1 ? `left: ${this.x}px;` : '';
			let top = this.y > -1 ? `top: ${this.y}px;` : '';
			return left + top;
		},
	},
	methods: {
		show(x = -1, y = -1) {
			this.x = x;
			this.y = y;
			this.status = true;
		},
		hide() {
			this.status = false;
		},
	},
	mounted() {
		try {
			const res = uni.getSystemInfoSync();
			console.log(res);
		} catch (e) {
			// error
		}
	},
};
</script>

<style></style>
