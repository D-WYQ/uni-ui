<template>
  <view>
    <view class="uni-padding-wrap uni-common-mt">
      <uni-segmented-control
        :current="current"
        :values="items"
        :style-type="styleType"
        :active-color="activeColor"
        @clickItem="onClickItem"/>
    </view>
    <view class="content">
      <view v-show="current === 0">选项卡1的内容</view>
      <view v-show="current === 1">选项卡2的内容</view>
      <view v-show="current === 2">选项卡3的内容</view>
    </view>

    <view class="example-title">Style</view>
    <view class="example-body">
      <radio-group
        class="uni-list "
        @change="styleChange">
        <label
          v-for="(item, index) in styles"
          :key="index"
          class="uni-list-item">
          <view class="uni-list-item__container">
            <view class="uni-list-item__content">
              <view class="uni-list-item__content-title">{{ item.text }}</view>
            </view>
            <view class="uni-list-item__extra"><radio
              :value="item.value"
              :checked="item.checked" /></view>
          </view>
        </label>
      </radio-group>
    </view>
    <view class="example-title">Color</view>
    <view class="example-body">
      <radio-group
        class="uni-list"
        @change="colorChange">
        <label
          v-for="(item, index) in colors"
          :key="index"
          class="uni-list-item">
          <view class="uni-list-item__container">
            <view class="uni-list-item__content"><view
              :style="{ backgroundColor: item }"
              class="color-tag"/></view>
            <view class="uni-list-item__extra"><radio
              :value="item"
              :checked="index === colorIndex" /></view>
          </view>
        </label>
      </radio-group>
    </view>
  </view>
</template>

<script>
export default {
  data () {
    return {
      items: ['选项卡1', '选项卡2', '选项卡3'],
      styles: [
        {
          value: 'button',
          text: '按钮',
          checked: true
        },
        {
          value: 'text',
          text: '文字'
        }
      ],
      colors: ['#007aff', '#4cd964', '#dd524d'],
      current: 0,
      colorIndex: 0,
      activeColor: '#007aff',
      styleType: 'button'
    }
  },
  methods: {
    onClickItem (index) {
      if (this.current !== index) {
        this.current = index
      }
    },
    styleChange (evt) {
      if (this.styleType !== evt.target.value) {
        this.styleType = evt.target.value
      }
    },
    colorChange (evt) {
      if (this.styleType !== evt.target.value) {
        this.activeColor = evt.target.value
      }
    }
  }
}
</script>

<style>
.uni-common-mt {
	margin-top: 20upx;
}
.content {
	display: flex;
	justify-content: center;
	align-items: center;
	height: 300upx;
	text-align: center;
}

.color-tag {
	width: 50upx;
	height: 50upx;
}

uni-radio-group uni-label {
	padding: 0;
}

.uni-list-item__container {
	padding: 24upx 30upx;
	width: 100%;
	box-sizing: border-box;
	flex: 1;
	position: relative;
	display: flex;
	flex-direction: row;
	justify-content: space-between;
	align-items: center;
}

.uni-list-item__container:after {
	position: absolute;
	z-index: 3;
	right: 0;
	bottom: 0;
	left: 30upx;
	height: 1px;
	content: '';
	-webkit-transform: scaleY(0.5);
	transform: scaleY(0.5);
	background-color: #c8c7cc;
}
.example-body {
	padding: 0;
}
.uni-list .uni-list-item:last-child {
}
</style>
