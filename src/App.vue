<template>
  <div class="page">
    <view class="navbar">
      <view class="nav-left">
        <view class="back-btn" @click="goBack">
          <text class="back-icon">‹</text>
        </view>
      </view>
      <view class="nav-center">
        <text class="nav-title">扩扩帮</text>
      </view>
      <view class="nav-right">
        <view class="more-btn">
          <text class="more-icon">⋯</text>
        </view>
      </view>
    </view>

    <view class="header-bg">
      <view class="header-top">
        <view class="logo-section">
          <img :src="logoImg" class="logo" />
          <text class="logo-text">扩扩帮</text>
        </view>
      </view>
      <view class="header-content">
        <text class="slogan">有问题，找朋友！</text>
        <text class="sub-slogan">真朋友，更愿意一起解决问题</text>
      </view>
    </view>

    <view class="profile-content">
        <view class="capsule-top">
          <view class="avatar-wrapper" @click="triggerUpload">
            <img :src="avatarImg || defaultAvatar" class="avatar" />
            <input type="file" accept="image/*" class="avatar-input" ref="fileInput" @change="uploadAvatar" />
          </view>
          <view class="name-area">
            <view class="name-row">
              <input type="text" class="nickname-input" v-model="nickname" maxlength="8" />
              <text class="ability-text">的能力图</text>
            </view>
          </view>
          <view class="change-btn" @click="triggerUpload">
            <text class="change-btn-text">更换头像 ></text>
          </view>
        </view>

        <view class="divider"></view>

        <view class="stats-row">
          <view class="stat-item">
            <view class="stat-circle">
              <img :src="statRingImg" class="stat-ring-bg" />
              <text class="stat-num">10</text>
            </view>
            <text class="stat-label">可求助好友</text>
          </view>
          <view class="stat-item">
            <view class="stat-circle">
              <img :src="statRingImg" class="stat-ring-bg" />
              <text class="stat-num">10</text>
            </view>
            <text class="stat-label">可提供帮助</text>
          </view>
          <view class="stat-item">
            <view class="stat-circle">
              <img :src="statRingImg" class="stat-ring-bg" />
              <text class="stat-num">0</text>
            </view>
            <text class="stat-label">获得点赞</text>
          </view>
        </view>
    </view>

    <view class="spacer"></view>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      nickname: '李雷',
      avatarImg: '',
      logoImg: require('@/assets/扩扩帮logo.png'),
      statRingImg: require('@/assets/能力图底盘.png')
    }
  },
  computed: {
    defaultAvatar() {
      const svg = `data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Ccircle cx='50' cy='50' r='48' fill='%23e8f0fe' stroke='%234296f5' stroke-width='1'/%3E%3Ccircle cx='50' cy='42' r='18' fill='%2390caf9'/%3E%3Ccircle cx='43' cy='38' r='2.5' fill='%23333'/%3E%3Ccircle cx='57' cy='38' r='2.5' fill='%23333'/%3E%3Cpath d='M 40 54 Q 50 64 60 54' stroke='%23666' stroke-width='2' fill='none' stroke-linecap='round'/%3E%3C/svg%3E`
      return svg
    }
  },
  methods: {
    goBack() {
      window.history.back()
    },
    uploadAvatar(event) {
      const file = event.target.files[0]
      if (file) {
        const reader = new FileReader()
        reader.onload = (e) => {
          this.avatarImg = e.target.result
        }
        reader.readAsDataURL(file)
      }
    },
    triggerUpload() {
      this.$refs.fileInput.click()
    }
  }
}
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.page {
  min-height: 100vh;
  background: url('~@/assets/bg.png') no-repeat center top / cover;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', sans-serif;
}

.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: 56px;
  background: rgba(255, 255, 255, 0.95);
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 16px;
  z-index: 100;
  backdrop-filter: blur(6px);
}

.nav-left, .nav-right {
  width: 44px;
  height: 44px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.nav-center {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
}

.back-btn, .more-btn {
  width: 36px;
  height: 36px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  cursor: pointer;
}

.back-btn:active, .more-btn:active {
  background: #f0f0f0;
}

.back-icon {
  font-size: 32px;
  color: #333;
  font-weight: 300;
  line-height: 1;
}

.more-icon {
  font-size: 20px;
  color: #666;
  letter-spacing: -2px;
}

.nav-title {
  font-size: 18px;
  font-weight: 600;
  color: #333;
}

.header-bg {
  padding-top: 56px;
  padding-left: 24px;
  padding-right: 24px;
  padding-bottom: 40px;
}

.header-top {
  display: flex;
  justify-content: flex-start;
  margin-bottom: 28px;
  padding-top: 16px;
}

.logo-section {
  display: flex;
  align-items: center;
}

.logo {
  width: 34px;
  height: 34px;
  margin-right: 8px;
}

.logo-text {
  font-size: 16px;
  font-weight: 600;
  color: #fff;
  letter-spacing: 1px;
}

.header-content {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.slogan {
  font-size: 34px;
  font-weight: 700;
  color: #fff;
  margin-bottom: 12px;
  letter-spacing: 3px;
  text-shadow: 0 1px 4px rgba(0, 0, 0, 0.15);
}

.sub-slogan {
  font-size: 15px;
  color: rgba(255, 255, 255, 0.9);
  letter-spacing: 2px;
  text-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.profile-content {
  margin: 0 20px;
  padding: 28px 24px;
  background: #f5f7fa;
  border-radius: 24px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
}

.capsule-top {
  display: flex;
  align-items: center;
}

.avatar-wrapper {
  position: relative;
  width: 64px;
  height: 64px;
  cursor: pointer;
  flex-shrink: 0;
}

.avatar {
  width: 100%;
  height: 100%;
  border-radius: 50%;
  object-fit: cover;
  border: 2px solid rgba(255, 255, 255, 0.8);
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
  display: block;
}

.avatar-input {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
  cursor: pointer;
}

.name-area {
  margin-left: 12px;
}

.name-row {
  display: flex;
  align-items: baseline;
}

.nickname-input {
  font-size: 20px;
  font-weight: 700;
  color: #1a2a3a;
  border: none;
  outline: none;
  background: transparent;
  width: 70px;
  padding: 0;
  line-height: 1.4;
}

.ability-text {
  font-size: 17px;
  font-weight: 500;
  color: #5a6a7a;
  white-space: nowrap;
  margin-left: 2px;
}

.change-btn {
  padding: 6px 12px;
  cursor: pointer;
  flex-shrink: 0;
  margin-left: auto;
}

.change-btn:active {
  background: rgba(255, 255, 255, 0.8);
}

.change-btn-text {
  font-size: 13px;
  color: #4a8af4;
  font-weight: 600;
  white-space: nowrap;
}

.divider {
  height: 1px;
  background: rgba(255, 255, 255, 0.6);
  margin: 20px 0 18px;
}

.stats-row {
  display: flex;
  justify-content: space-around;
  align-items: center;
}

.stat-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  flex: 1;
}

.stat-circle {
  position: relative;
  width: 80px;
  height: 80px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.stat-ring-bg {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
}

.stat-num {
  position: relative;
  font-size: 28px;
  font-weight: 800;
  color: #3b7cf5;
  line-height: 1;
  z-index: 1;
}

.stat-label {
  font-size: 13px;
  color: #6a7a8a;
  margin-top: 8px;
  font-weight: 500;
}

.spacer {
  height: 40px;
}
</style>
