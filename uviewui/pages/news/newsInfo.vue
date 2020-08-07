<template>
	<!-- <view> 收到的参数为：{{paramsStr.age}}</view> -->
	<web-view :webview-styles="webviewStyles" :src="id"></web-view>
</template>


<script>
	export default {
		data() {
			return {
				id: "",
				params: {}

			}
		},
		onLoad(option) {
			this.params = option;
			this.id  = this.params.age;
		},
		computed: {
			paramsStr() {
				return this.params;
			}
		},

		methods: {


		}
	};
</script>



<style lang="scss" scoped>

</style>
