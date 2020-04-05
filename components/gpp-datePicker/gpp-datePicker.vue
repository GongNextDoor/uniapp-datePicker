<template>
	<view class="gpp-datePicker" @click.stop="show">
		<slot />
		<view class="g-dp-mask" :class="{'show':pipkerShowFlag}" @click.stop="hide" @touchmove.stop.prevent catchtouchmove="true"></view>
		<view class="g-dp-content" :class="{'show':pipkerShowFlag}" @touchmove.stop.prevent catchtouchmove="true">
			<view class="g-dp-ctt-head">
				<view class="g-dp-ctt-hd-btn" @click.stop="onCancel">取消</view>
				<view class="g-dp-ctt-hd-btn" :style="{'color':themeColor}" @click.stop="onConfirm">确定</view>
			</view>
			<view class="g-dp-ctt-wrapper">
				<picker-view :indicator-style="indicatorStyle" :value="selectedValue" @change="wrapperChange">
					<picker-view-column>
						<view class="g-dp-ctt-wp-item" v-for="(item,index) in years" :key="index">{{item}}年</view>
					</picker-view-column>
					<picker-view-column>
						<view class="g-dp-ctt-wp-item" v-for="(item,index) in months" :key="index">{{item}}月</view>
					</picker-view-column>
					<picker-view-column>
						<view class="g-dp-ctt-wp-item" v-for="(item,index) in days" :key="index">{{item}}日</view>
					</picker-view-column>
				</picker-view>
			</view>
		</view>
	</view>
</template>

<script>
	import gppDatePicker from "./gpp-datePicker.js";
	export default {
		props: {
			themeColor:{
				type:String,
				default(){
					return "#6ba1ff"
				}
			},
			defaultValue:{
				type:String,
				default(){
					return this.getNowDate()
				}
			},
			startDate:{
				type:String,
				default(){
					return "1900-01-01"
				}
			},
			endDate:{
				type:String,
				default(){
					return "2100-12-31"
				}
			}
		},
		data() {
			return {
				pipkerShowFlag: false,
				indicatorStyle: `height: ${uni.upx2px(88)}px;`,
				
				selectedValue: [],
				
				years: [],
				months: [],
				days: []
			}
		},
		watch: {
			defaultValue:function(newVal, oldVal){
				this.init();
			},
			startDate:function(newVal, oldVal){
				this.init();
			},
			endDate:function(newVal, oldVal){
				this.init();
			}
		},
		created() {
			this.init();
		},
		methods: {
			init(){
				this.getYears();
				this.getMonth(this.defaultValue);
				const date = new Date()
				        for (let i = 1; i <= 31; i++) {
				            this.days.push(i)
				        }
				this.showPicker(this.defaultValue);
			},
			
			show(){
				this.pipkerShowFlag = true;
			},
			hide(){
				this.pipkerShowFlag = false;
			},
			onCancel(){
				this.pipkerShowFlag = false;
				this.$emit("onCancel", {
					dateValue: this.selectedDate
				});
			},
			onConfirm(){
				this.pipkerShowFlag = false;
				this.$emit("onConfirm", {
					dateValue: this.selectedDate
				});
			},
			
			wrapperChange(e){
				let selectedDate = this.years[e.detail.value[0]]+"-"+this.months[e.detail.value[1]]+"-"+this.days[e.detail.value[2]];
				this.getMonth(selectedDate);
			},
			getYears(){
				let startDateArray = this.startDate.split("-");
				let endDateArray = this.endDate.split("-");
				let startYear = Number(startDateArray[0]);
				let endYear = Number(endDateArray[0]);
				
				let newYears = []
				for(let i=startYear; i<=endYear; i++){
					newYears.push(i);
				}
				this.years = newYears;
			},
			getMonth(nowDate){
				let startDateArray = this.startDate.split("-");
				let endDateArray = this.endDate.split("-");
				let nowDateArray = nowDate.split("-");
				let startYear = Number(startDateArray[0]);
				let endYear = Number(endDateArray[0]);
				let startMonth = Number(startDateArray[1]);
				let endMonth = Number(endDateArray[1]);
				
				let newMonths = [];
				if(startYear != Number(nowDateArray[0])){
					for(let i=1; i<=12; i++){
						newMonths.push(i);
					}
				}else{
					for(let i=startMonth; i<=endMonth; i++){
						newMonths.push(i);
					}
				}
				this.months = newMonths;
			},
			
			getNowDate(){
				let date = new Data();
				let year = data.getFullYear();
				let month = date.getMonth+1;
				let day = date.getDay();
				
				return year+"-"+this.dateFormate(month)+"-"+this.dateFormate(day);
			},
			dateFormate(val){
				if(Number(val) > 9){
					return val;
				}
				return "0"+val;
			},
			showPicker(showDate){
				let showArray = [0,0,0];
				let showDateArray = showDate.split("-");
				this.years.forEach((el, index) => {
					if(Number(showDateArray[0]) == el){
						showArray[0] = index;
						return false;
					}
				})
				this.months.forEach((el, index) => {
					if(Number(showDateArray[1]) == el){
						showArray[1] = index;
						return false;
					}
				})
				this.days.forEach((el, index) => {
					if(Number(showDateArray[2]) == el){
						showArray[2] = index;
						return false;
					}
				})
				this.selectedValue = showArray;
			}
		}
	}
</script>

<style lang="scss">
	.gpp-datePicker{
		position: relative;
		z-index: 99;
		.g-dp-mask{
			position: fixed;
			z-index: 100;
			top: 0;
			right: 0;
			left: 0;
			bottom: 0;
			background: rgba(0, 0, 0, 0.6);
			visibility: hidden;
			opacity: 0;
			transition: all 0.3s ease;
		}
		.g-dp-mask.show{
			visibility: visible;
			opacity: 1;
		}
		.g-dp-content{
			position: fixed;
			z-index: 101;
			bottom: 0;
			right: 0;
			width: 100%;
			transition: all 0.3s ease;
			transform: translateY(100%);
			.g-dp-ctt-head{
				height: 88upx;
				background-color: #FFFFFF;
				border-bottom: 1px solid #e5e5e5;
				padding: 0 40upx;
				display: flex;
				align-items: center;
				justify-content: space-between;
				.g-dp-ctt-hd-btn{
					color: #888;
					font-size: 17px;
				}
			}
			.g-dp-ctt-wrapper{
				height: 480upx;
				width: 100%;
				background-color: #FFFFFF;
				.g-dp-ctt-wp-item{
					text-align: center;
					width: 100%;
					height: 88upx;
					line-height: 88upx;
					text-overflow: ellipsis;
					white-space: nowrap;
					font-size: 30upx;
				}
			}
		}
		.g-dp-content.show{
			transform: translateY(0);
		}
		uni-picker-view{
			height: 100%;
		}
	}
</style>
