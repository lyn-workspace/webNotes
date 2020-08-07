<template>
	<view>
		<u-search placeholder="日照香炉生紫烟" v-model="keyword" @search="toSearch"></u-search>

		<u-tabs :list="tabs" :is-scroll="false" :current="current" @change="change"></u-tabs>
		<u-card v-for="(article, index) in articles" :key="article.title">
			<view class="" slot="body" @click="toArticleInfo(article.id)">
				<view class="top">
					<view class="left">
						<u-icon name="list" :size="30" color="rgb(94,94,94)"></u-icon>
						<view class="store">{{ article.title}}</view>
					</view>
				</view>

				<view class="u-body-item u-flex u-border-bottom u-col-between u-p-t-0">
					<view class="u-body-item-title u-line-2" v-text="article.desp">瓶身描绘的牡丹一如你初妆，冉冉檀香透过窗心事我了然，宣纸上走笔至此搁一半</view>

					<image src="https://img11.360buyimg.com/n7/jfs/t1/94448/29/2734/524808/5dd4cc16E990dfb6b/59c256f85a8c3757.jpg"
					 mode="aspectFill"></image>
				</view>
				<view>

					<!-- 标签;-->
					<u-tag v-for="tag in article.tags" :text="tag.name" mode="light" shape="circle" type="warning" :key="tag.id" />

				</view>
			</view>



			<view class="" slot="foot">
				<u-icon name="eye" size="34" color="" :label="`发布时间   :`+article.createTime"></u-icon>

				<text class=""> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</text>
				<u-icon name="eye" size="34" color="" :label="article.view+'人观看'"></u-icon>
			</view>
		</u-card>
		<!-- 	<view class="item u-border-bottom" v-for="(item, index) in list" :key="index">
			{{'第' + item + '条数据'}}
		</view> -->
		<u-loadmore :status="status" :load-text="loadText" bgColor="#f2f2f2"></u-loadmore>
	</view>

</template>

<script>
	export default {
		data() {
			return {
				loadText: {
					loadmore: '轻轻上拉',
					loading: '努力加载中',
					nomore: '实在没有了'
				},
				tabs: [{
						name: "最新"
					},
					{
						name: "最热"
					}

				],
				status: 'loadmore',
				list: 15,
				page: 0,
				current: 0,

				articles: [{
						id: 1,
						title: '素胚勾勒出青花，笔锋浓转淡',
						subTitle: '2020-05-15',
						desp: '瓶身描绘的牡丹一如你初妆，冉冉檀香透过窗心事我了然，宣纸上走笔至此搁一半',
						thumb: 'http://pic2.sc.chinaz.com/Files/pic/pic9/202002/hpic2119_s.jpg',
						view: 20,
						createTime: '2019-04-04 12:12',
						tags: [{
							"name": "张三",
							"id": 2
						}, {
							"name": "张三",
							"id": 3
						}, {
							"name": "张三",
							"id": 4
						}, {
							"name": "张三",
							"id": 5
						}]
					}

				],
				keyword: '',

			};
		},
		onLoad() {

		},

		computed: {

		},
		onReachBottom() {
			if (this.page >= 3) return;
			this.status = 'loading';
			this.page = ++this.page;
			setTimeout(() => {
				for (let i = 0; i < 5; i++) {
					let article = this.articles[0];
					article.id = this.$u.random(0, this.articles.length - 1);
					this.articles.push(article)
				}


				if (this.page >= 3) {
					this.status = 'nomore';;

				} else {
					this.status = 'loading';
				}
			}, 2000)
		},
		methods: {
			// //分页,加载更多
			// reachBottom() {
			// 	console.log("加载数据");
			// 	// 此tab为空数据
			// 		// setTimeout(() => {
			// 			// this.getArticleList(this.current);
			// 		// }, 100);
			// },
			// getArticleList(page) {

			// 	for (let i = 0; i < 5; i++) {
			// 		this.articles.push(this.articles[0]);
			// 	}
			// 	this.status =  "loadmore";

			// },
			change(index) {
				this.current = index;
			},
			toSearch(value) {
				console.log("111");
				// 跳转搜索结果页面
				alert("111:" + value)
			},
			toArticleInfo(id) {

				alert("跳转详情, id:" + id)
			}
		}
	};
</script>

<style>
	/* #ifndef H5 */
	page {
		height: 100%;
		background-color: #f2f2f2;
	}

	/* #endif */
</style>

<style lang="scss" scoped>
	.u-card-wrap {
		background-color: $u-bg-color;
		padding: 1px;
	}

	.u-body-item {
		font-size: 32rpx;
		color: #333;
		padding: 20rpx 10rpx;
	}

	.u-body-item image {
		width: 120rpx;
		flex: 0 0 120rpx;
		height: 120rpx;
		border-radius: 8rpx;
		margin-left: 12rpx;
	}

	.top {
		display: flex;
		justify-content: space-between;

		.left {
			display: flex;
			align-items: center;

			.store {
				margin: 0 10rpx;
				font-size: 32rpx;
				font-weight: bold;
			}
		}

		.right {
			color: $u-type-warning-dark;
		}
	}
</style>
