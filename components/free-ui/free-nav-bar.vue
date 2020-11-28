<template>
	<view >
		<view class="bg-light" :class="fixed ? 'fixed-top' : ''">
			<!-- 状态栏 -->
			<view :style="'height: ' + statusBarHeight + 'px;'"></view>
			<!-- 导航 -->
			<view style="height: 90rpx;" class="w-100 flex align-center justify-between">
				<!-- 左边 -->
				<view class="flex align-center font-md">
					<!-- 标题 -->
					<text class="font-md ml-3"><slot name="title"></slot></text>
				</view>
				<!-- 右边 -->
				<view class="flex align-center">
					<free-icon-button :icon="'\ue6e3'" @click="handleBtnClick"></free-icon-button>
					<free-icon-button :icon="'\ue682'" @click="handleBtnClick"></free-icon-button>
				</view>
			</view>
		</view>
		<!-- 占位 -->
		<view v-if="fixed" :style="fixedStyle"></view>
	</view>
</template>

<script>
import freeIconButton from '@/components/free-ui/free-icon-button.vue';
export default {
	components: {
		freeIconButton
	},
	props: {
		title: {
			type: Boolean,
			default: false
		},
		fixed: {
			type: Boolean,
			default: true,
		},
	},
	data() {
		return {
			statusBarHeight: 0,
			navBarHeight: 0,
		};
	},
	computed: {
		fixedStyle() {
			return `height: ${this.navBarHeight}px;`
		}
	},
	mounted() {
		// #ifdef APP-PLUS-NVUE
		this.statusBarHeight = plus.navigator.getStatusbarHeight();
		// #endif
		this.navBarHeight = this.statusBarHeight + uni.upx2px(90);
	},
	methods: {
		handleBtnClick() {
			console.log('btn click');
		}
	}
};
</script>

<style></style>
