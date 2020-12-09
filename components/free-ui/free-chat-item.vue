<template>
	<view>
		<!-- 时间显示 -->
		<view v-if="showTime" class="flex align-center justify-center pb-4 pt-2"><text class="font-sm text-light-muted">{{showTime}}</text></view>
		<!-- 气泡 -->
		<view class="flex align-start position-relative mb-3" :class="isself ? 'justify-end' : 'justify-start'">
			<!-- 好友 -->
			<template v-if="!isself">
				<free-avatar size="70" :src="item.avatar"></free-avatar>
			</template>
			<text class="iconfont font-md position-absolute" :class="isself ? 'text-chat-item chat-right-icon' : 'text-white chat-left-icon'">{{ isself ? '&#xe640;' : '&#xe609;' }}</text>
			<div class="rounded p-2 " style="max-width:500rpx;" :class="isself ? 'bg-chat-item mr-3' : 'bg-white ml-3'">
				<text class="font-md">{{ item.data }}</text>
			</div>
			<!-- 本人 -->
			<template v-if="isself">
				<free-avatar size="70" :src="item.avatar"></free-avatar>
			</template>
		</view>
	</view>
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
		preTime: [Number,String],
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
		}
	}
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
</style>
