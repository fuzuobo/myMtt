<template>
 <div id="wo">
   <label>  
    <h3>开始时间</h3>  
    <input type="text" id="publish_start_time" @click="openPicker" v-text="publish_start_time">  
    <span>至</span>  
    <input type="text" id="publish_end_time" @click="openPicker" v-text="publish_end_time">  
  </label>  
  
        <!--  
            v-model 属性为组件的绑定值  
            type 属性表示 datetime-picker 组件的类型，它有三个可能的值：  
                datetime: 日期时间选择器，可选择年、月、日、时、分，value 值为一个 Date 对象  
                date: 日期选择器，可选择年、月、日，value 值为一个 Date 对象  
                time: 时间选择器，可选择时、分，value 值为一个格式为 HH:mm 的字符串  
              
            @confirm 回调绑定事件，还有一个取消的事件，api并没有注明，可以用@cancle="取消后的事件名"  


			  type="date"
			  year-format="{value} 年"
			  month-format="{value} 月"
			  date-format="{value} 日"
      -->  
      <!--  <mt-datetime-picker ref="picker" v-model="pickerValue" type="date" @confirm="handleConfirm" ></mt-datetime-picker>  --> 

      <mt-datetime-picker ref="picker" v-model="pickerValue" type="datetime" @confirm="handleConfirm" ></mt-datetime-picker>  
      
    </div>
  </template>

  <script>

    export default {
     name: 'wo',
     data(){
      return{
		     pickObj: "", //当前选择时间的对象  
                pickerValue: new Date(), // 选择时间的值  
                publish_start_time: "", //绑定表单的开始时间的值  
                publish_end_time: "", //绑定表单的结束时间的值  
              }
            },
            methods: {
             openPicker(event) {  
                  // 打开时间选择器  
                  this.$refs.picker.open();  
                this.pickObj = event.target; //使用当前对象赋值，以便于在回调中将值传输进去  
              },  
              handleConfirm() {  
                 //选择时间后的回调  
                let data = this.formatDate(this.pickerValue); //使用formatDate格式化输出  
                this.pickObj.value = data; //将选择的value值，传进表单中  
              },
              formatDate(date) {  
              // 格式化日期为 y-m-d H:i:s  
              var y = date.getFullYear();  
              var m = date.getMonth() + 1;  
              var mm = m < 10 ? ('0' + m) : m;  
              var d = date.getDate();  
              var dd = d < 10 ? ('0' + d) : d;  
              var h = date.getHours();  
              var hh = h < 10 ? ('0' + h) : h;  
              var minute = date.getMinutes();  
              var minuteminute = minute < 10 ? ('0' + minute) : minute;  
              var second = date.getSeconds();  
              var secondsecond = second < 10 ? ('0' + second) : second;  
              return y + '-' + m + '-' + d + ' ' + h + ':' + minute + ':' + second;  
            }

          },
          components: {

          }
        }
      </script>

      <style>

      </style>
