<template>
	<div @longpress="long">
		<!-- 时间显示 -->
		<view v-if="showTime" class="flex align-center justify-center pb-4 pt-2">
			<text class="font-sm text-light-muted">{{ showTime }}</text>
		</view>
		<!-- 撤回消息 -->
		<view v-if="item.isremove" ref="isremove" class="flex align-center justify-center pb-4 pt-1"><text class="font-sm text-light-muted">你撤回了一条信息</text></view>
		<!-- 气泡 -->
		<view v-else class="flex align-start position-relative mb-3" :class="isself ? 'justify-end' : 'justify-start'">
			<!-- 好友 -->
			<template v-if="!isself">
				<free-avatar size="70" :src="item.avatar"></free-avatar>
			</template>
			<text class="iconfont font-md position-absolute" :class="isself ? 'text-chat-item chat-right-icon' : 'text-white chat-left-icon'">
				{{ isself ? '&#xe640;' : '&#xe609;' }}
			</text>
			<div class="rounded p-2 " style="max-width:500rpx;" :class="isself ? 'bg-chat-item mr-3' : 'bg-white ml-3'">
				<text class="font-md">{{ item.data }}</text>
			</div>
			<!-- 本人 -->
			<template v-if="isself">
				<free-avatar size="70" :src="item.avatar"></free-avatar>
			</template>
		</view>
	</div>
</template>

<script>
import freeAvatar from '@/components/free-ui/free-avatar.vue';
import $T from '@/common/free-lib/time.js';

export default {
	components: { freeAvatar },
	props: {
		item: Object,
		index: Number,
		// 上一条消息的时间戳
		preTime: [Number, String],
	},
	computed: {
		// 是否是本人
		isself() {
			// 获取本人id (假设拿到了)
			let id = 1;
			return this.item.user_id === id;
		},
		// 显示的时间
		showTime() {
			return $T.getChatTime(this.item.create_time, this.preTime);
		},
	},
	methods: {
		// 长按事件
		long(e) {
			let x = 0;
			let y = 0;
			// #ifdef APP-PLUS-NVUE
			if (Array.isArray(e.changedTouches) && e.changedTouches.length > 0) {
				x = e.changedTouches[0].screenX;
				y = e.changedTouches[0].screenY;
			}
			// #endif
			// #ifdef MP
			x = e.detail.x;
			y = e.detail.y;
			// #endif
			this.$emit('long', { x, y, index: this.index });
		},
	},
	mounted() {
		// 监听是否撤回消息
		this.$watch('item.isremove', (newVal, oldVal) => {
			if (newVal) {
				// #ifdef APP-PLUS-NVUE
				const animation = weex.requireModule('animation');
				this.$nextTick(() => {
					animation.transition(
						this.$refs.isremove,
						{
							styles: {
								opacity: 1,
							},
							duration: 1000,
							timingFunction: 'ease',
						},
						() => {}
					);
				});
				// #endif
			}
		});
	},
};
</script>

<style scoped>
.chat-left-icon {
	left: 80rpx;
	top: 20rpx;
}
.chat-right-icon {
	right: 80rpx;
	top: 20rpx;
}
.chat-animate {
	/* #ifdef APP-PLUS-NVUE */
	opacity: 0;
	/* #endif */
}
</style>
