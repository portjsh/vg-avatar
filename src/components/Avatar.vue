<template>
  <div class="hello">
    <div class="leaderboard">
      <div class="intro" v-if="currentStep == 0">
        <p class="text-center dark-gray">
          <strong class="ng-binding">See how you stack up!</strong>
        </p>
        <p
          class="text-center light dark-gray ng-binding"
        >With Leaderboard, you can see how many blocks similar Brand Representatives are completing. Do your best to make it to the top of the group!</p>
        <button class="outline default full-width ng-binding" @click="changeStep(1)">TRY IT OUT!</button>
        <!-- <span class="little-text">{{txc.leaderboardDisclaimer}}</span> -->
      </div>

      <!-- Step ONE -->
      <div v-if="currentStep == 1" class="ng-hide">
        <strong class="ng-binding">We're excited to have you!</strong>
        <p></p>
        <p class="ng-binding">First, pick a display name:</p>
        <label for="display_name" class="ng-binding">Display Name</label>
        <input
          id="display_name"
          type="text"
          class="lb-text-box ng-pristine ng-untouched ng-valid"
          ng-model="userData.displayName"
        >
        <p class="text-center">
          <strong class="ng-binding">Can't think of a display name? Let us help!</strong>
        </p>
        <div class="button-wrapper">
          <button class="outline purple ng-binding" ng-click="generateName()">GENERATE DISPLAY NAME</button>
        </div>
        <p
          class="little-text ng-binding"
        >*This will be displayed publicly, so please remember that it must contain appropriate language and content, and if it references an individual’s identity, then that individual must be named on the Brand Affiliate Account.</p>

        <button class="outline default" @click="changeStep(0)">Back</button>
        <button class="solid default" @click="changeStep(2)">Continue</button>
      </div>
      <div v-if="currentStep == 2">
        <p class="ng-binding">Next, choose a picture to use:</p>
        <div class="avatars">
          <img
            v-for="avatar in avatars"
            :key="avatar.id"
            :src="'https://www.nuskin.com/vg/avatars/avatar'+ avatar.id+'.svg'"
            :class="{selected:avatar.id == id}"
            class="avatar"
            :data-avatar="avatar.id"
            @click="$set(id = avatar.id)"
          >
        </div>
        <button class="outline default" @click="changeStep(1)">Back</button>
        <button class="solid default" @click="save()">Save</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "avatarWizard",
  props: {
    msg: String
  },
  data() {
    return {
      currentStep: 0,
      avatars: [],
      id: 6
    };
  },
  methods: {
    changeStep(step) {
      // console.log("New step", step);
      this.currentStep = step;
    },
    save(avatar) {
      this.avatar = {
        avatarName: avatarName,
        id: id
      };
    }
    // selectAvatar() {
    //   this.selected = !this.selected;
    // }
  },
  mounted() {
    this.avatars = [];
    for (var i = 1; i <= 36; i++) {
      this.avatars.push({
        id: i
      });
    }
    console.log(this.avatars);
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.leaderboard .avatars {
  height: 300px;
  border: 1px solid #bbbcbc;
  padding: 10px 10px 0 10px;
  overflow-y: scroll;
  margin-top: 20px;
  border-radius: 5px;
}
.leaderboard .avatars .avatar {
  border-radius: 50%;
  margin: 5px;
  width: 50px;
}
.leaderboard .avatars .avatar:hover {
  cursor: pointer;
}
.leaderboard .avatars .avatar.selected,
.leaderboard .avatars .avatar.notSelected:hover {
  opacity: 1;
}
.leaderboard .avatars .avatar:not(.selected) {
  opacity: 0.4;
}
.leaderboard .terms {
  height: 300px;
  border: 1px solid #bbbcbc;
  padding: 10px 10px 0 10px;
  overflow-y: scroll;
  margin-top: 20px;
  border-radius: 5px;
}
.leaderboard .terms a {
  color: #008ab0;
  text-decoration: underline;
}
.leaderboard .button-wrapper,
.leaderboard .text-center {
  text-align: center;
}
.leaderboard .footer-buttons {
  display: flex;
  flex-flow: row nowrap;
  align-items: center;
  justify-content: space-between;
}
.leaderboard button {
  font-size: 24px;
  cursor: pointer;
  outline: none;
}
.leaderboard button.full-width {
  width: 100%;
}
.leaderboard button.outline,
.leaderboard button.solid {
  line-height: 4px;
  padding: 10px;
  border: 1px solid #272525;
  min-height: 36px;
  font-size: 16px;
  min-width: 48%;
  border-radius: 10px;
  margin-top: 20px;
  margin-bottom: 20px;
}
.leaderboard button.outline,
.leaderboard button.solid {
  margin-right: 10px;
}
.leaderboard button.solid {
  background: #272525;
  color: white;
}
.leaderboard button.purple {
  color: #6521d4;
  border-color: #6521d4;
  font-size: 16px;
  margin: 0 auto;
  min-height: 0;
  padding: 15px;
  text-align: center;
  float: none;
}
.leaderboard button.purple:hover {
  background: #dbcaf7;
}
.leaderboard button:disabled {
  background: #dcd9d9;
  border: 1px #c1bcbc solid;
  cursor: none;
}
.leaderboard .leaderboard-list {
  padding: 0;
}
.leaderboard .leaderboard-list.top-leaders {
  box-shadow: inset 0 20px 60px -20px rgba(163, 163, 163, 0.8);
  border-bottom: 3px solid #e7e7e7;
}
.leaderboard .leaderboard-list .leader-item {
  display: flex;
  flex-flow: row nowrap;
  justify-content: flex-start;
  align-items: center;
  padding: 10px 0 10px 20px;
}
.leaderboard .leaderboard-list .leader-item .number {
  padding-right: 15px;
  color: #bbbcbc;
  min-width: 25px;
  text-align: center;
}
.leaderboard .leaderboard-list .leader-item .avatar img {
  border-radius: 50%;
  margin-right: 15px;
  height: 50px;
  width: 50px;
}
.leaderboard .leaderboard-list .leader-item .display-name {
  color: #272525;
}
.leaderboard .leaderboard-list .leader-item .display-name .edit {
  display: none;
}
.leaderboard .leaderboard-list .leader-item .display-name .area {
  display: block;
  color: #a7a7a7;
  font-weight: 300;
  font-size: 14px;
  margin-top: 5px;
}
.leaderboard .leaderboard-list .leader-item .blocks {
  display: flex;
  margin-left: auto;
  align-self: center;
  margin-right: 20px;
}
.leaderboard .leaderboard-list .leader-item .blocks img {
  margin-right: 10px;
}
.leaderboard .leaderboard-list .leader-item.highlighted {
  border-left: 3px solid #35b2f0;
  background: #d7f0fb;
  background: linear-gradient(to right, #d7f0fb 0%, #fbfbfb 85%);
  filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#d7f0fb', endColorstr='#fbfbfb',GradientType=1 );
}
.leaderboard .leaderboard-list .leader-item.highlighted .number {
  color: #272525;
}
.leaderboard .leaderboard-list .leader-item.highlighted .blocks {
  color: #35b2f0;
}
.leaderboard .leaderboard-list .leader-item.highlighted .blocks img {
  -webkit-filter: invert(0.08) sepia(1) saturate(8) hue-rotate(175deg);
  filter: invert(0.08) sepia(1) saturate(8) hue-rotate(175deg);
}
.leaderboard .leaderboard-list .leader-item.highlighted:hover .edit {
  display: inline-flex;
  color: #35b2f0;
}
.leaderboard .leaderboard-list .leader-item.highlighted:hover .edit:hover {
  cursor: pointer;
}
.leaderboard .median-blocks {
  padding-top: 20px;
}
.leaderboard .median-blocks a {
  color: #008ab0;
  text-decoration: underline;
}
</style>
