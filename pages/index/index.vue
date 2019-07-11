<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view>
			<text class="title">{{title}}</text>
            <str-autocomplete :stringList="stringList" :importvalue="title" @select="selectOne" highlightColor="#FF0000" v-model="title"></str-autocomplete>
			<view class="button-area">
				<button class="primary" @click="changeTitle('test')">测试</button>
				<button class="primary" @click="changeTitle('hi')">还原</button>
			</view>
			
		</view>
	</view>
</template>

<script>
    import strAutocomplete from '@/components/str-autocomplete/str-autocomplete.vue'
	export default {
        components: {
            strAutocomplete
        },
		data() {
            return {
                title: 'Hello',
                stringList: ['apple', 'string', 'delicious', 'everything', 'somethingWrong','中古国']
            }
        },
		onLoad() {

		},
		methods: {
    
            selectOne(opt) {
				this.title = opt
                console.log(opt)
            },
			changeTitle(text) {
				this.title = text
			}
		}
	}
</script>

<style lang="scss">
	.content {
		text-align: center;
		height: 400upx;
	}

	.logo {
		height: 200upx;
		width: 200upx;
		margin-top: 200upx;
	}

	.title {
		font-size: 36upx;
		color: #8f8f94;
	}
	.button-area {
		width: 80%;
		margin: 300px auto 0;
		.primary {
			color: blue;
			margin: 10px;
		}
	}
</style>
