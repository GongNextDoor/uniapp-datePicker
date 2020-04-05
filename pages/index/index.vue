<template>
	<view class="content">
		<view class="text-area">
			<gpp-date-picker @onCancel="onCancel" @onConfirm="onConfirm" :startDate="startDate" :endDate="endDate" :defaultValue="pickerDate">
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
				startDate: "2018-05-02",
				endDate: "2022-09-20",
				pickerDate: '2020-11-25'
			}
		},
		methods: {
			onCancel(e){
				console.log(e);
			},
			onConfirm(e){
				this.pickerDate = e.dateValue;
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
