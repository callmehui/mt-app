<template>
  <div class="star">
    <span class="star-item" v-for="(itemClass, index) in itemClasses" :key="index" :class="itemClass"></span>
  </div>
</template>

<script>

// 星星的长度
const   LENGTH = 5

// 星星状态（显示黄星星、灰色星星还是半星星）
const CLS_ON = 'on'
const CLS_HALF = 'half'
const CLS_OFF = 'off'

export default {
  props: {
    score:{
      type: Number
    }
  },
  computed: {
    itemClasses(){
      let result = []

      // 配置星星分数（为4或者4.5这种，即都转换为0.5的倍数）
      let score = Math.floor( this.score * 2 ) / 2

      // 是否有半星
      let hasDecimal = score % 1 !== 0

      // 全星
      let integer = Math.floor(score)

      // 遍历全星
      for(let i = 0; i < integer; i++ ){
        result.push( CLS_ON );
      }

      // 向数组插入半星（如果存在）
      if(hasDecimal){
        result.push(CLS_HALF)
      }

      // 补齐:当全星和半星都添加进数组后，剩余的加上灰色的星星；eg: ["on","on","half","off","off"]
      while(result.length < LENGTH){
        result.push(CLS_OFF)
      }

      console.log(result)

      return result

    }
  }
}
</script>

<style scoped>
.star{
		font-size: 0;
	}
	.star .star-item{
		display: inline-block;
		width: 10px;
		height: 10px;
		margin-right: 3px;
		background-repeat: no-repeat;
		background-size: 10px 10px;
	}
	.star .star-item:last-child{
		margin-right: 0;
	}

	/* 三种图片类型*/
	.star .on{
		background-image: url(img/star24_on@2x.png);
	}
	.star .half{
		background-image: url(img/star24_half@2x.png);
	}
	.star .off{
		background-image: url(img/star24_off@2x.png);
	}
</style>
