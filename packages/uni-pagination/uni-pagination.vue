<template>
  <view class="uni-pagination">
    <view class="uni-pagination__btns">
      <view
        :class="['uni-pagination__btn',{'uni-pagination--disabled':currentIndex === 1}]"
        :hover-class="currentIndex === 1 ? '' : 'uni-pagination--hover'"
        :hover-start-time="20"
        :hover-stay-time="70"
        @click="clickLeft">
        <template v-if="showIcon===true || showIcon === 'true'">
          <uni-icon
            color="#000"
            size="20"
            type="arrowleft"/>
        </template>
        <template v-else>
          {{ prevText }}
        </template>
      </view>
      <view
        :class="['uni-pagination__btn',{'uni-pagination--disabled':currentIndex === maxPage}]"
        :hover-class="currentIndex === maxPage ? '' : 'uni-pagination--hover'"
        :hover-start-time="20"
        :hover-stay-time="70"
        @click="clickRight">
        <template v-if="showIcon===true || showIcon === 'true'">
          <uni-icon
            color="#000"
            size="20"
            type="arrowright"/>
        </template>
        <template v-else>
          {{ nextText }}
        </template>
      </view>
    </view>
    <view class="uni-pagination__num">
      <text class="uni-pagination__num-current">{{ currentIndex }}</text>/{{ maxPage }}
    </view>
  </view>
</template>

<script>
import uniIcon from '../uni-icon/uni-icon.vue'
export default {
  name: 'UniPagination',
  components: {
    uniIcon
  },
  props: {
    prevText: {
      type: String,
      default: '上一页'
    },
    nextText: {
      type: String,
      default: '下一页'
    },
    current: {
      type: [Number, String],
      default: 1
    },
    total: { // 数据总量
      type: [Number, String],
      default: 0
    },
    pageSize: { // 每页数据量
      type: [Number, String],
      default: 10
    },
    showIcon: { // 是否以 icon 形式展示按钮
      type: [Boolean, String],
      default: false
    }
  },
  data () {
    return {
      currentIndex: 1
    }
  },
  computed: {
    maxPage () {
      let maxPage = 1
      let total = Number(this.total)
      let pageSize = Number(this.pageSize)
      if (total && pageSize) {
        maxPage = Math.ceil(total / pageSize)
      }
      return maxPage
    }
  },
  watch: {
    current (val) {
      this.currentIndex = +val
    }
  },
  created () {
    this.currentIndex = +this.current
  },
  methods: {
    clickLeft () {
      if (Number(this.currentIndex) === 1) {
        return
      }
      this.currentIndex -= 1
      this.change('prev')
    },
    clickRight () {
      if (Number(this.currentIndex) === this.maxPage) {
        return
      }
      this.currentIndex += 1
      this.change('next')
    },
    change (e) {
      this.$emit('change', {
        type: e,
        current: this.currentIndex
      })
    }
  }
}
</script>

<style lang="scss">
	@mixin pagination-disabled {
		opacity: 0.3;
	}

	@mixin pagination-hover {
		color: rgba(0, 0, 0, .6);
		background-color: $uni-bg-color-hover;
	}

	.uni-pagination {
		width: 100%;
		box-sizing: border-box;
		padding: 0 40upx;
		position: relative;
		overflow: hidden;
		display: flex;
		flex-direction: row;

		&__btns {
			flex: 1;
			display: flex;
			justify-content: space-between;
			align-items: center;
			flex-direction: row;
		}

		&__btn {
			width: 120upx;
			height: 60upx;
			padding: 0 16upx;
			line-height: 60upx;
			font-size: $uni-font-size-base;
			box-sizing: border-box;
			position: relative;
			background-color: #f8f8f8;
			display: flex;
			flex-direction: row;
			justify-content: center;
			align-items: center;

			&:after {
				content: "";
				width: 200%;
				height: 200%;
				position: absolute;
				top: 0;
				left: 0;
				border: 1px solid $uni-border-color;
				transform: scale(.5);
				transform-origin: 0 0;
				box-sizing: border-box;
				border-radius: $uni-border-radius-lg;
			}
		}

		&__num {
			width: 100upx;
			height: 60upx;
			line-height: 60upx;
			font-size: $uni-font-size-base;
			color: $uni-text-color;
			position: absolute;
			left: 50%;
			top: 0;
			transform: translateX(-50%);

			&-current {
				color: $uni-color-primary;
			}
		}

		&--disabled {
			@include pagination-disabled;
		}

		&--hover {
			@include pagination-hover;
		}
	}
</style>
