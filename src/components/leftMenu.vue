<template>
  <nav>
    <ul class="main_menu">
      <!-- 선택한 메뉴 li.is-current // 뎁스 공통 -->
      <!-- 서브메뉴 있으면 li.is-sub 추가해주세요 -->
      <li class="home is-current">
        <a href="javascript:void(0);">HOME</a>
      </li>
      <li class="sales is-sub">
        <a href="#">매출관리</a>
        <ul class="sub_menu">
          <li><router-link to="/Sale01">매출관리</router-link></li>
          <li><router-link to="/Sale02">이용현황</router-link></li>
        </ul>
      </li>
      <li class="customer is-sub">
        <a href="javascript:void(0);">고객관리</a>
        <ul class="sub_menu">
          <li><router-link to="/Customer01">회원조회</router-link></li>
          <li><router-link to="/Customer02">Fleet차량관리</router-link></li>
          <li><router-link to="/Customer03">멤버쉽조회</router-link></li>
          <li><router-link to="/Customer04">멤버쉽구독결제</router-link></li>
          <li><router-link to="/Customer05">멤버쉽알림톡발송</router-link></li>
          <li><router-link to="/Customer06">공지사항</router-link></li>
        </ul>
      </li>
      <li class="promotion is-sub">
        <a href="javascript:void(0);">프로모션</a>
        <ul class="sub_menu">
          <li><router-link to="/Promotion01">프로모션관리</router-link></li>
          <li><router-link to="/Promotion02">쿠폰관리</router-link></li>
          <li><router-link to="/Promotion03">쿠폰발행</router-link></li>
          <li><router-link to="/Promotion04">Gift Card 교환</router-link></li>
        </ul>
      </li>
      <li class="product is-sub">
        <a href="javascript:void(0);">상품관리</a>
        <ul class="sub_menu">
          <li><router-link to="/Product01">상품조회</router-link></li>
          <!-- <li><router-link to = "/Product02">진열관리(상품)</router-link></li>
                          <li><router-link to = "/Product03">진열관리(옵션)</router-link></li> -->
        </ul>
      </li>
      <li class="equipment is-sub">
        <a href="javascript:void(0);">장비제어</a>
        <ul class="sub_menu">
          <!-- <li><router-link to = "/Equ01">장비제어</router-link></li> -->
          <li><router-link to="/Equ02">세차순서</router-link></li>
          <!-- <li><router-link to = "/Equ03">이용현황</router-link></li> -->
        </ul>
      </li>
      <li class="basics is-sub">
        <a href="javascript:void(0);">기초관리</a>
        <ul class="sub_menu">
          <!-- <li><router-link to = "/Setting01">계정생성</router-link></li> -->
          <li><router-link to="/Setting02">근무자관리</router-link></li>
          <!-- <li><router-link to = "/Setting03">장비/단말기 관리</router-link></li>
                          <li><router-link to = "/Setting04">기초코드관리</router-link></li> -->
        </ul>
      </li>
    </ul>
    <div class="info">
      <p>(주)엔티아이</p>
      사업자등록번호 : 504-81-15358 ㅣ 대표이사 : 김도연<br>대구광역시 서구 와룡로 335 1층 스파크플러스
    </div>
  </nav>
</template>

<script>
export default {
  name: 'leftMenu',
  components: {
  },
  data() {
    return {

    }
  }
}
</script>