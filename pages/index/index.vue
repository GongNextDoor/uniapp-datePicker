<template>
	<view class="content">
		<view class="text-area">
			<gpp-date-picker @onCancel="onCancel" startDate="2009-05-02" defaultValue="2020-04-22">
				<text class="title">{{pickerDate}}</text>
			</gpp-date-picker>
		</view>
	</view>
</template>

<script>
	import gppDatePicker from "../../components/gpp-datePicker/gpp-datePicker.vue"
	export default {
		components:{
			gppDatePicker
		},
		data() {
			return {
				pickerDate: '2020-11-25'
			}
		},
		onLoad() {

		},
		methods: {
			onCancel(e){
				console.log(e);
			}
		}
	}
</script>

<style>
	.content {
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.text-area {
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
