<template>
<div class="lg:flex">
  <div class="lg:w-1/2 xl:max-w-screen-sm">
    <div class="mt-8 px-12 sm:px-24 md:px-48 lg:px-12 lg:mt-8 xl:px-24 xl:max-w-2xl">
      <h2 class="text-center text-3xl text-color-1 font-display font-semibold lg:text-left xl:text-3xl
                    xl:text-bold">JOIN</h2>
      <div class="mt-12">
        <form v-if="globalShare.isLogined == false" v-on:submit.prevent="checkAndJoin">
          <div>
            <div class="text-sm font-bold text-gray-700 tracking-wide">ID</div>
            <input ref="loginIdElRef" class="w-full text-lg py-2 border-b border-gray-300 focus:outline-none focus:border-blue-900" type="text" placeholder="Enter your ID">
          </div>
          <div class="mt-8">
            <div class="text-sm font-bold text-gray-700 tracking-wide">password</div>
            <input ref="loginPwElRef" class="w-full text-lg py-2 border-b border-gray-300 focus:outline-none focus:border-blue-900" type="password" placeholder="Enter your password">
          </div>
          <div class="mt-8">
            <div class="text-sm font-bold text-gray-700 tracking-wide">passwordConfirm</div>
            <input ref="loginPwConfirmElRef" class="w-full text-lg py-2 border-b border-gray-300 focus:outline-none focus:border-blue-900" type="password" placeholder="Enter your passwordConfirm">
          </div>
          <div class="mt-8">
            <div class="text-sm font-bold text-gray-700 tracking-wide">name</div>
            <input ref="nameElRef" class="w-full text-lg py-2 border-b border-gray-300 focus:outline-none focus:border-blue-900" type="text" placeholder="Enter your name">
          </div>
          <div class="mt-8">
            <div class="text-sm font-bold text-gray-700 tracking-wide">nickname</div>
            <input ref="nicknameElRef" class="w-full text-lg py-2 border-b border-gray-300 focus:outline-none focus:border-blue-900" type="text" placeholder="Enter your nickname">
          </div>
          <div class="mt-8">
            <div class="text-sm font-bold text-gray-700 tracking-wide">Email Address</div>
            <input ref="emailElRef" class="w-full text-lg py-2 border-b border-gray-300 focus:outline-none focus:border-blue-900" type="email" placeholder="Enter your Email Address">
          </div>
          <div class="mt-8">
            <div class="text-sm font-bold text-gray-700 tracking-wide">cellphoneNo</div>
            <input ref="cellphoneNoElRef" class="w-full text-lg py-2 border-b border-gray-300 focus:outline-none focus:border-blue-900" type="tel" placeholder="Enter your cellphoneNo">
          </div>

          <div class="mt-10">
            <button type="submit" value="가입" class="login-btn bg-main text-gray-100 p-4 w-full rounded-full tracking-wide
                                font-semibold font-display focus:outline-none focus:shadow-outline
                                shadow-lg">
              join
            </button>
          </div>
        </form>
        <div v-else>
          이미 로그인 되었습니다. <router-link class="btn-link" to="/">홈</router-link> 으로 이동
        </div>

        <div class="mt-12 text-sm font-display font-semibold text-gray-700 text-center">
          SNS로 계정으로 간편하게 가입하세요..
          <div class="icon-block flex justify-center mt-8 text-4xl">
            <div class="mr-8"><a href="#" class="hover:bg-opacity-80 bg-yellow-200 w-20 h-20 block rounded-full flex justify-center items-center"><i class="fas fa-comment"></i></a></div>
            <div><a href="#" class="hover:bg-opacity-80 bg-green-600 text-white w-20 h-20 block rounded-full flex justify-center items-center"><span>N</span></a></div>
          </div>

        </div>

      </div>
    </div>
  </div>
  <div class="hidden lg:flex items-center justify-center bg-blue-100 flex-1 h-screen sticky top-0 left-0">
    <div class="max-w-md transform duration-200 hover:scale-110 cursor-pointer">
      <div class="">
        <img class="" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FSo8Ix%2Fbtq1FA0n54L%2FeKnOyBlr436oPK3p8w9fs0%2Fimg.png" alt="">
      </div>
    </div>
  </div>
</div>  
</template>

<script lang="ts">
import { defineComponent, ref, reactive, getCurrentInstance, onMounted } from 'vue'
import { MainApi } from '../apis/'
import { Router } from 'vue-router';
export default defineComponent({
  name: 'MemberJoinPage',
  props: {
    globalShare: {
      type: Object,
      required: true
    },
  },
  setup(props) {
    const router:Router = getCurrentInstance()?.appContext.config.globalProperties.$router;
    const mainApi:MainApi = getCurrentInstance()?.appContext.config.globalProperties.$mainApi;
    const loginIdElRef = ref<HTMLInputElement>();
    const loginPwElRef = ref<HTMLInputElement>();
    const loginPwConfirmElRef = ref<HTMLInputElement>();
    const profileImgElRef = ref<HTMLInputElement>();
    const nameElRef = ref<HTMLInputElement>();
    const nicknameElRef = ref<HTMLInputElement>();
    const cellphoneNoElRef = ref<HTMLInputElement>();
    const emailElRef = ref<HTMLInputElement>();
    
    function checkAndJoin() {
      // 로그인아이디 체크
      if ( loginIdElRef.value == null ) {
        return;
      }
      const loginIdEl = loginIdElRef.value;
      loginIdEl.value = loginIdEl.value.trim();
      if ( loginIdEl.value.length == 0 ) {
        alert('로그인 아이드를 입력해주세요.');
        loginIdEl.focus();
        return;
      }
      // 로그인비번 체크
      if ( loginPwElRef.value == null ) {
        return;
      }
      const loginPwEl = loginPwElRef.value;
      loginPwEl.value = loginPwEl.value.trim();
      if ( loginPwEl.value.length == 0 ) {
        alert('로그인 비번을 입력해주세요.');
        loginPwEl.focus();
        return;
      }
      // 로그인비번확인 체크
      if ( loginPwConfirmElRef.value == null ) {
        return;
      }
      const loginPwConfirmEl = loginPwConfirmElRef.value;
      if ( loginPwEl.value != loginPwConfirmEl.value ) {
        alert('로그인 비번이 일치하지 않습니다.');
        loginPwConfirmEl.focus();
        return;
      }
      // 이름 체크
      if ( nameElRef.value == null ) {
        return;
      }
      const nameEl = nameElRef.value;
      nameEl.value = nameEl.value.trim();
      if ( nameEl.value.length == 0 ) {
        alert('이름을 입력해주세요.');
        nameEl.focus();
        return;
      }
      // 별명 체크
      if ( nicknameElRef.value == null ) {
        return;
      }
      const nicknameEl = nicknameElRef.value;
      nicknameEl.value = nicknameEl.value.trim();
      if ( nicknameEl.value.length == 0 ) {
        alert('별명을 입력해주세요.');
        nicknameEl.focus();
        return;
      }
      // 휴대전화번호 체크
      if ( cellphoneNoElRef.value == null ) {
        return;
      }
      const cellphoneNoEl = cellphoneNoElRef.value;
      cellphoneNoEl.value = cellphoneNoEl.value.trim();
      if ( cellphoneNoEl.value.length == 0 ) {
        alert('휴대전화번호를 입력해주세요.');
        cellphoneNoEl.focus();
        return;
      }
      // 이메일 체크
      if ( emailElRef.value == null ) {
        return;
      }
      const emailEl = emailElRef.value;
      emailEl.value = emailEl.value.trim();
      if ( emailEl.value.length == 0 ) {
        alert('이메일을 입력해주세요.');
        emailEl.focus();

        return;
      }
      const startJoin = (genFileIdsStr:string) => {
        join(loginIdEl.value, loginPwEl.value, nameEl.value, nicknameEl.value, cellphoneNoEl.value, emailEl.value, genFileIdsStr);
      };
      const startFileUpload = (onSuccess:Function) => {
        if ( !!!profileImgElRef.value?.files ) {
          onSuccess("");
          return;
        }
        
        mainApi.common_genFile_doUpload(profileImgElRef.value?.files[0])
          .then(axiosResponse => {
            if ( axiosResponse.data.fail ) {
              alert(axiosResponse.data.msg);
              return;
            }
            else {
              onSuccess(axiosResponse.data.body.genFileIdsStr);
            }
          });
      };
      startFileUpload(startJoin);
    }
    function join(loginId:string, loginPw:string, name:string, nickname:string, cellphoneNo:string, email:string, genFileIdsStr:string) {
      mainApi.member_doJoin(loginId, loginPw, name, nickname, cellphoneNo, email, genFileIdsStr)
        .then(axiosResponse => {
          alert(axiosResponse.data.msg);
          if ( axiosResponse.data.fail ) {
            return;
          }
          router.replace('/member/login?loginId=' + loginId)
        });
    }
    return {
      checkAndJoin,
      loginIdElRef,
      loginPwElRef,
      profileImgElRef,
      loginPwConfirmElRef,
      nameElRef,
      nicknameElRef,
      cellphoneNoElRef,
      emailElRef,
    }
  }
})
</script>

<style scoped>
</style>