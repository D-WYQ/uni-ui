<template>

  <view class="uni-navbar">
    <view
      :class="{'uni-navbar--fixed': fixed,'uni-navbar--shadow':border,'uni-navbar--border':border}"
      :style="{'background-color':backgroundColor}"
      class="uni-navbar__content">
      <uni-status-bar v-if="statusBar"/>
      <view
        :style="{color:color}"
        class="uni-navbar__header uni-navbar__content_view">
        <view
          class="uni-navbar__header-btns uni-navbar__content_view"
          @tap="onClickLeft">
          <view
            v-if="leftIcon.length"
            class="uni-navbar__content_view">
            <uni-icon
              :type="leftIcon"
              :color="color"
              size="24"/>
          </view>
          <view
            v-if="leftText.length"
            :class="{'uni-navbar-btn-icon-left':!leftIcon.length}"
            class="uni-navbar-btn-text uni-navbar__content_view">{{ leftText }}</view>
          <slot name="left"/>
        </view>
        <view class="uni-navbar__header-container uni-navbar__content_view">
          <view
            v-if="title.length"
            class="uni-navbar__header-container-inner uni-navbar__content_view">{{ title }}</view>
          <!-- 标题插槽 -->
          <slot/>
        </view>
        <view
          class="uni-navbar__header-btns uni-navbar__content_view"
          @tap="onClickRight">
          <view
            v-if="rightIcon.length"
            class="uni-navbar__content_view">
            <uni-icon
              :type="rightIcon"
              :color="color"
              size="24"/>
          </view>
          <!-- 优先显示图标 -->
          <view
            v-if="rightText.length&&!rightIcon.length"
            class="uni-navbar-btn-text uni-navbar__content_view">{{ rightText }}</view>
          <slot name="right"/>
        </view>
      </view>
    </view>
    <view
      v-if="fixed"
      class="uni-navbar__placeholder">
      <uni-status-bar v-if="statusBar"/>
      <view class="uni-navbar__placeholder-view"/>
    </view>
  </view>
</template>

<script>
import uniStatusBar from '../uni-status-bar/uni-status-bar.vue'
import uniIcon from '../uni-icon/uni-icon.vue'

export default {
  name: 'UniNavBar',
  components: {
    uniStatusBar,
    uniIcon
  },
  props: {
    title: {
      type: String,
      default: ''
    },
    leftText: {
      type: String,
      default: ''
    },
    rightText: {
      type: String,
      default: ''
    },
    leftIcon: {
      type: String,
      default: ''
    },
    rightIcon: {
      type: String,
      default: ''
    },
    fixed: {
      type: [Boolean, String],
      default: false
    },
    color: {
      type: String,
      default: '#000000'
    },
    backgroundColor: {
      type: String,
      default: '#FFFFFF'
    },
    statusBar: {
      type: [Boolean, String],
      default: false
    },
    shadow: {
      type: [String, Boolean],
      default: true
    },
    border: {
      type: [String, Boolean],
      default: true
    }
  },
  methods: {
    onClickLeft () {
      this.$emit('click-left')
    },
    onClickRight () {
      this.$emit('click-right')
    }
  }
}
</script>

<style lang="scss">
	$nav-height:44px;

	.uni-navbar {
		&__content {
			display: block;
			position: relative;
			width: 100%;
			background-color: $uni-bg-color;
			overflow: hidden;

			.uni-navbar__content_view {
				// line-height: $nav-height;
				display: flex;
				align-items: center;
			}
		}

		&__header {
			display: flex;
			flex-direction: row;
			width: 100%;
			height: $nav-height;
			line-height: $nav-height;
			font-size: 16px;

			&-btns {
				display: inline-flex;
				flex-wrap: nowrap;
				flex-shrink: 0;
				width: 120upx;
				padding: 0 12upx;

				&:first-child {
					padding-left: 0;
				}

				&:last-child {
					width: 60upx;
				}
			}

			&-container {
				width: 100%;
				margin: 0 10upx;

				&-inner {
					width: 100%;
					display: flex;
					justify-content: center;
					font-size: 30upx;
					padding-right: 60upx;
				}
			}
		}

		&__placeholder {
			&-view {
				height: $nav-height;
			}
		}

		&--fixed {
			position: fixed;
			z-index: 998;
		}

		&--shadow {
			box-shadow: 0 1px 6px #ccc;
		}

		&--border:after {
			position: absolute;
			z-index: 3;
			bottom: 0;
			left: 0;
			right: 0;
			height: 1px;
			content: '';
			-webkit-transform: scaleY(.5);
			transform: scaleY(.5);
			background-color: $uni-border-color;
		}
	}
</style>
