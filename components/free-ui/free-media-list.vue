<template>
	<view class="flex align-center align-stretch" hover-class="bg-light">
		<view class="flex align-center justify-center position-relative" style="width: 145rpx;">
			<free-avatar :src="item.avatar" size="92"></free-avatar>
			<free-badge v-if="item.noreadnum" badgeClass="position-absolute" badgeStyle="top:15rpx;right:15rpx;">
				<text class="text-white font-sm">{{ item.noreadnum }}</text>
			</free-badge>
		</view>
		<view class="flex flex-1 flex-column border-bottom py-3 pr-3 border-light-secondary">
			<view class="flex align-center justify-between mb-1">
				<text class="font-md">{{ item.nickname }}</text>
				<text class="font-sm text-light-muted">{{ item.update_time | formatTime }}</text>
			</view>
			<text class="font text-ellipsis text-light-muted">{{ item.data }}</text>
		</view>
	</view>
</template>

<script>
import $Time from '@/common/free-lib/time.js';
import freeAvatar from '@/components/free-ui/free-avatar.vue';
import freeBadge from '@/components/free-ui/free-badge.vue';
export default {
	components: {
		freeAvatar,
		freeBadge
	},
	props: {
		item: Object,
		index: Number
	},
	filters: {
		formatTime(value) {
			return $Time.gettime(value);
		}
	}
};
</script>

<style></style>
