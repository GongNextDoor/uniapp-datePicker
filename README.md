# gpp-uniapp-datePicker
#### 日期选择器
风格与官方日期选择器统一，解决官方日期选择器设置startDate，endDate后超出范围日期依然会显示问题。并且天数显示为当月真实天数。
#### 使用方式
引用组件
```javascript
import gppDatePicker from "@/components/gpp-datePicker/gpp-datePicker.vue"
export default {
	components:{
		gppDatePicker
	}
}
```
使用组件
```html
<gpp-date-picker @onCancel="onCancel" @onConfirm="onConfirm" :startDate="startDate" :endDate="endDate" :defaultValue="pickerDate">
	{{pickerDate}}
</gpp-date-picker>
```
```javascript
export default {
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
```
#### 属性说明
| 属性名 | 类型 | 默认值 | 说明 |
| ------------ | ------------ | ------------ | ------------ |
| themeColor | String | #6ba1ff | 主题色（确认按钮颜色） |
| defaultValue | String | 当前日期 | 初始选中日期（格式为标准yyyy-MM-dd格式） |
| startDate | String | 1900-01-01 | 起始日期（格式为标准yyyy-MM-dd格式） |
| endDate | String | 2100-12-31 | 结束日期（格式为标准yyyy-MM-dd格式） |
#### 事件说明
| 事件名称 | 说明 | 返回值 |
| ------------ | ------------ | ------------ |
| onCancel | 点击取消触发 | {dateValue: "2018-09-30", dateValueIndex: [0, 4, 29]} |
| onConfirm | 点击确认触发 | {dateValue: "2018-09-30", dateValueIndex: [0, 4, 29]} |
#### 注意事项
组件初始化时会对props值进行校验，列如传入错误日期格式，起始日期晚于结束日期等则不会进行初始化并弹窗提示。
