<script>
export default {
	onLaunch() {
		// #ifdef APP-PLUS-NVUE
		const domModule = weex.requireModule('dom');
		domModule.addRule('fontFace', {
			fontFamily: 'iconfont',
			src: "url('https://at.alicdn.com/t/font_1365296_2ijcbdrmsg.ttf')",
		});
		// #endif
		console.log('App Launch');
	},
	onShow() {
		console.log('App Show');
	},
	onHide() {
		console.log('App Hide');
	}
};
</script>

<style>
/*每个页面公共css */
@import './common/free.css';
@import './common/common.css';
/* #ifndef APP-PLUS-NVUE */
@import './common/free-icon.css';
/* #endif */
</style>
