<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view>
			<text class="title">{{title}}</text>
            <str-autocomplete :stringList="stringList" @select="selectOne" highlightColor="#FF0000" v-model="title"></str-autocomplete>
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
                console.log(opt)
            }
		}
	}
</script>

<style>
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
</style>
