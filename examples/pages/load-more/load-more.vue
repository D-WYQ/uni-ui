<template>
  <view>
    <view class="example-info">加载更多组件用于页面加载更多数据时，页面底部显示内容等场景。</view>
    <view class="example-title">基本用法</view>
    <view class="example-body">
      <uni-load-more :status="status"/>
    </view>
    <view class="example-title">修改默认颜色及文字</view>
    <view class="example-body">
      <uni-load-more
        :status="status"
        :content-text="contentText"
        color="#007aff"/>
    </view>

    <view class="example-title">改变组件状态</view>
    <radio-group
      class="uni-list"
      @change="onChange">
      <label
        v-for="(item, index) in statusTypes"
        :key="index"
        class="uni-list-item">
        <view class="uni-list-item__container">
          <view class="uni-list-item__content">
            <view class="uni-list-item__content-title">{{ item.text }}</view>
          </view>
          <view class="uni-list-item__extra">
            <radio
              :value="item.value"
              :checked="item.checked" />
          </view>
        </view>
      </label>
    </radio-group>
  </view>
</template>
<script>
export default {
  data () {
    return {
      status: 'more',
      statusTypes: [{
        value: 'more',
        text: '加载前',
        checked: true
      }, {
        value: 'loading',
        text: '加载中',
        checked: false
      }, {
        value: 'noMore',
        text: '没有更多',
        checked: false
      }],
      contentText: {
        contentdown: '查看更多',
        contentrefresh: '加载中',
        contentnomore: '没有更多'
      }
    }
  },
  methods: {
    onChange (e) {
      this.status = e.detail.value
    }
  }
}
</script>

<style>
	uni-radio-group uni-label {
		padding: 0;
	}
	.uni-list {
		background: #fff;
	}
	.example-body {
		padding: 10upx 30upx;
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
		-webkit-transform: scaleY(.5);
		transform: scaleY(.5);
		background-color: #c8c7cc;
	}
</style>
