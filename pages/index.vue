<template>
  <!-- <Tutorial/> -->
  <div
    id="app"
  >
    <Flipbook
      class="flipbook"
      :pages="pictures"
      :singlePage="true"
      v-slot="flipbook"
      ref="flipbook"
    >
      <div class="action-bar">
        <outline-arrow-circle-left-icon 
          class="w-10 h-10 btn left" 
          v-if="true === false"
          :class="{ disabled: !flipbook.canFlipLeft }"
          @click="FlipLeft"
        />
        <outline-zoom-in-icon 
          class="w-10 h-10 btn plus" 
          v-if="true === false"
          :class="{ disabled: !flipbook.canZoomIn }"
          @click="ZoomIn"
        />
        <span class="page-info">
          <b>
            Memories <br />
            #DevFestLAGOS 2021
          </b>
        </span>
        <outline-zoom-out-icon 
          class="w-10 h-10 btn minus" 
          v-if="true === false"
          :class="{ disabled: !flipbook.canZoomOut }"
          @click="ZoomOut"
        />
        <outline-arrow-circle-right-icon 
          class="w-10 h-10 btn right" 
          v-if="true === false"
          :class="{ disabled: !flipbook.canFlipRight }"
          @click="FlipRight"
        />
      </div>
    </Flipbook>
  </div>
</template>

<script>
export default {
  name: "App",
  data () {
    return {
      xDown: null,
      yDown: null,
      pictures: [
        null,
        "https://lh3.googleusercontent.com/G79uGba1MrXbUHKeYsIMFINoiqmnLFQK4_qapNeShUDJw0MF4cCzxlYd6bn90ybiTC-FfC4G14sBxm5HCq0x4trO7k8uar5xq4EkehwCouJJz33TtPpiAu5pVE0oLrV3TEn4QCHbO28",
        "https://lh3.googleusercontent.com/OVwmfjBXmMxd9wVvPC-T31-O6KMMoogDQoS8gPTVsYHjLEvP8WuMPcXhjcMMyI_WnQTdayErJFdvdWKdb6GPmMmoBCJcnrUauLYNDhjs2O_4ihky2K4ONom6zxNM7cxJRoxeq3CMIBI",
        "https://lh3.googleusercontent.com/sL_M0Lp41gQ7bGQSUuvxDSxa4W9NHrog8nhXbCFogVLoKXcJV8VrksZhRAS9qgazbp4gTkOqJheA1EWxO-CmQVsfbW51wPgVqe6QT3eeUjC1eGCcztKBCpqUV-uvk9TMiboebSM9Qsg",
        "https://lh3.googleusercontent.com/KsWDV1BML2AubeaGrI07C5XwcKPr4DiSQ3dLYXdS7Dbqm530dNbxwR4fRatIHOxb2WgTQr1dB2UlY4X0QIjhtw6T6naP7j-tLc9txMJCg2Mxi-B0yHNiHw6PqhCh81rzbfaUY7tDoMg",
        "https://lh3.googleusercontent.com/sXMminPSZ0pVm2gV4MXRoTC1r7z1TOMINPHehcSL0SXaxNM5lPqzj4_hzS0OW6Lsfc1VGPishB4W0lIrPH-8qpi3WWjwOii0aLdehn_ns86k-Su-myopnBs7mEwyANB50lbfQ-smnAE",
        "https://lh3.googleusercontent.com/xCs2b7I9H5OYpIBhiPqfD4mMO1HaipsVnTwmKDUUITmMrAILub6rVUX5fIjcA09cDJGZfXJHedsSBfrtL21tlTB4XzjP_PYGBOe5Vjt6KECwnS2t_oHweGOo-T-xegdXMO09Oc7SNiE",
        "https://lh3.googleusercontent.com/rLf-nuBfkGbMBD3uqDSScaZmX-2WE9aGJsg5yNxATGb5v1ggrgGSLXGnJTy-IHRnMjojHy9yuyqznRHNQTrVKuV-cv6ehk7ual1hCketxKriiZHemTFxJZy9kT9ydDHFDEXym5b8k20",
        "https://lh3.googleusercontent.com/fA8qomSqMjTD1Inb8tQ36fo3WSHdPkYGOFPiX-xGy-eChfzNbE2fq6aoxruGER8dEHawEAL08HvEUcorUYbOdp295drfg5TQxgM03hNDDOa1H7L8fWRaa6IGVYUh6vMAz7-y8-y9pw8",
        "https://lh3.googleusercontent.com/7X0q9yME1KN2odEqqkAb2QqccbyMvWQuPGM6wI6C5fxiX0H9sbJIQqCFdrW6W5hdu7NO1tNDar-2IVTUgKN1t3CIkYk0lPSLwRFiaXurzjjxL0nsomGA_GhWRFiwkebBymra4XYs4Oo",
        "https://lh3.googleusercontent.com/qqwfJwVIWGsmNt2AGuZkB1HcS2MY-mFZRwCUVo3HPEp2HVdh4emb_2TQFaTv42jz5zmVTJbe6L11k9M8M4uE_k2zFDMC99P18pJocmjsaPvXzZhOkyKfRPq2ee6Z4Ct5ORGBmlloqDs",
        "https://lh3.googleusercontent.com/WhaZBi8gxW-h5twXsWxAMOUBtnoIi5HNOwRVE0qXeCuXBQGC9YN_Z8XC8CFVH137tJsykIBzYwp7FknAPS2Ykptdacu5BFczpZNzBfv_Qz8ezIuRvDYWhACrYdaOb76FNS4Z4KW5dDk",
        "https://lh3.googleusercontent.com/yE0jr_Qtr5-wELEtTE620QAMZn8NU4LbVJdg6tIDmEdtRR_wb8rzMiq0W4P0yfNsjD05heps2juLKUYX7WWhntKvx-WXV4GSNwjeIrAEBLE3bI-4ifymnNukBFAyu17qVh18-UHi9TY",
        "https://lh3.googleusercontent.com/aJEhYeOMSnxmOC0_25tYuTELK0pfNdsp27Ppgybebgnjh3YTKJME_hW2RhCG39ndDKV-8ZoFKbjoYBcoRQwwXhU-mfnO-S7BhJkyy_ZLccFQtsjzgygeqIi_EvWfoT7SVdXD1QQNBB8",
        "https://lh3.googleusercontent.com/WwIwFVIX0BbU8uct8fTsk3X86hSOXqfWBuPt1lHcLq49YLXAZNOqTzMksD7MFyTjyHClEYUHkOYbpvZO7w9SkKFlB0EJa0g6PZJawQY2v1mD04e3xH2iP-v8svu7ZoO9QbpYrun4MJ8",
        "https://lh3.googleusercontent.com/HEs8CZYAaLr9URE8eObAVlKPVElp7k9mmu8N-gh-Q82gIK6DuzSyysSurp-OIcRkBkDAPK7kZMRb_cwS5TjXZf7uiMBaI0RcUZZB0tYWWXCVvrPxcxnxIzrfr7mpOq5rOrfKJ_t0OAw",
        "https://lh3.googleusercontent.com/9v6IvMWNKpfMINMnVYPXyR9SIqPc6Q5lOkFiZ8qNj1hMv40B_RiFPNM2jdyY5xESjID2kSULJNUXJp7r4gIXgkgRp4YhkmFEzUBadCGYDE-5dP1AkD2PnnuGjUryfKpPB8A8XYYHDKc",
        "https://lh3.googleusercontent.com/n9x-9SUMCzj31OkiCNx18KnYqgfhBft8XzaO5ljk6kJ2izv_A0NQYapKoRq3zC9tO7PF7tSsS4errdiOgOXQGQhLr8-cKm6waU0ZiZyC7yodgWy_BPcZOyS9qiKKaPMmZ1q4n3ekyIw",
        "https://lh3.googleusercontent.com/_euSYkDDnv1Ssq7qKoY16muTFWcgE-tzdxwxA2Ib0xRjj2kLY_d8Gq2dDIY0N4kYdtdteyUUszvRxaK6UNMDs-RQ7DVnt_hm03DFB-9DqRY5n2MrTU8s-hYzvIk6ARIA4S9wPvj2wh8",
        "https://lh3.googleusercontent.com/W0Z7RB1EzcuUwzoAaqNfG2OPCzqJFFftGTnD-HQral1n3l0mfPcb7ohae3Y6kIDP0EVOMUeiHk5GOuYmrTWbwWPVpf7AyKSe8kHrC9BfoMwzEN2G7x6i8ipbwHYfeMOSnvq6uWOdotU",
        "https://lh3.googleusercontent.com/TBcoKrUL0Ih_ZmutbQFuaO9aQGUMN-8x8zMlQBzWj5jMbDP6hQLTAiNAc8EB_tEii36FzHoV4_CZLkZStzshw9u-fHBxcIsVD2qxhSTWoztq1j0sJOSvYTAHTH4Iet3QzllxCMRPTwI",
        "https://lh3.googleusercontent.com/p0iTFESuvI0PS1Kwq24VmaLcenas7GJPD-y8DvF5ftWyj_B9q2ttZmD-9rfOLdIHu4yLk4Q-McXOx3QB7A9vvnfwNRE-FdJjXqC3kuDwt2KFy_Dq8V8aLPsss_Ky_y7uwbghxNMbwHs",
        "https://lh3.googleusercontent.com/LTJxucb6Qojkj6yWRY8TDZQK8ODp0_fk1q9dK1rg5IhRB5Q1I2Z1uLU3Qh_bT1D5zY0XKHKCFp8xsnpAif4AqzKRsnhWxVJxcypNUaIgdj5-rhj2zrqdqcRNUyCuaedP8VOgO1JmpqA",
        "https://lh3.googleusercontent.com/_ocOvrmlgH2J22_Pw3g7eOPIdzPdrPuKIRDyhHuTszjsKV3BRmnmBDkNoaS0pzkZusaX-pILCdHNINt4C2TIdK2GW-evBbviNi3UCVEWAjXObyNrmEF597hV1Iu4o1JPpGd67hN5tsk",
        "https://lh3.googleusercontent.com/smi8ft7_Lf6IjDu0xD_j0vhwOAqBzSnLtnFM7iBYpsVVoE4NLiYev7w4cwUtLI6cswtXfwL6NPiYKmju9-YdcauzgwcaumiQHHxHX_FwhI0zy5ga184XFgWNgjMkswTm5-vT1Wn8AMk",
        "https://lh3.googleusercontent.com/AfsWLo5-31DrizQ3-GemCckHu4uz8GD4lms9xCXKaBF6aC7efEPrKspB-LSF8HoXKEGagp4ec0V6FFhN1c1f4-b1DNEKeDtpfmCFQ10TQYXGMHlWwDP7p3EZ5JXPAA-9u6puxOOqDy4",
        "https://lh3.googleusercontent.com/jkrwuwQyUPARK9_tf4cr1NC3ZS2NSjjNg3cd8Ko2BohUs4DCe2ms69HuCa4oewopUaM_Gk7BinZ17qvc1GBHMZ7EKAGqWHlq14FHyRKVxSMMmRM8UBErrPaDehtDiQu5mZJ0UkaYGDQ",
        "https://lh3.googleusercontent.com/KpuqcJo1VAfkXzFhdrnYKrjZBCh-fFavXH08p-undAssVfDtyhFdN83SyNGuSScbyj-fOJjaqJ_5GDVcx07C7OFPDHPNVl3DINPF_7wk9OK03RVZgQOADp12qGYfrPIVqdlRYi513Cg",
        "https://lh3.googleusercontent.com/e_83PQSz9gSPwRljvLCGkzWGJF9JnmlugxXmvvTZlfBsGAOvvBFDerQ9Vwr6qYlgUnHfFE7gRjZ4FLys__WA7L3vnQGnl5YEaXFzhbmKGn02O6977LAmbrZmecjTJVzjz99iAU8gIvE",
        "https://lh3.googleusercontent.com/OChc4-hgFZg9V0gaxRDR4kSZJe7BrKKu_RteDB6oo6v4NL04-7jg2xwNVnyo7el_PCv0SCWaWiuTh7khRXXfmJahWRxwvgip5SKNS6Z5jn0kVRpMtbRf6eChhDgIvu8AB9-ePQ4GoK8",
        "https://lh3.googleusercontent.com/st7O7aiqcYpBMX9c0pNpPelntp4DmsNBu6lkrEt4p65HsnjTwPTaOdw2b6wPBebHjS_O6iyegl8NXLuJ1Z3GCDc-hzvvR8DhkkniQ8ULU2DL5uz0oUi0kDMlN3pBtHwDFvYaMcFOy90",
        "https://lh3.googleusercontent.com/pzb_M_ESUBVjZOIBAsugdFnoPVx-J6-P5ytvfHngHo9OzPLjoMl65jgapBrii14ZfSUKu3oVBv2eNN974d-zODhlZoT_OaZzefdePTi1XiMbL3QW5rY2symElu-1GJiEU8Rh3s3lC5w",
        "https://lh3.googleusercontent.com/DLNY3ik34l1RD-pElF5D9Ay-h5_DmRJI7pZtunxDwgCSu2Fm0vO9YRJ3YwhGPNc52FT_izIfy1LTJnWhosX0hXM-NjMvGCbEUyUU_3pOU_wTvUL0RJxXZs0y88gd6mqjh6-RmdO49pE",
        "https://lh3.googleusercontent.com/aMqi56yJzsr-MXb8dwz6OkpRl3KW1umlckiQ55_rrfAXJp045kk8z7QwB8u4EzsOvH6bZ43R0oq3-5BVDwN6Syqy2E8wo7wIkAH63JXqPMHHXYpJdU5SkdP7CjxUSSwVpP5Zj34Su8g",
        "https://lh3.googleusercontent.com/o_3uh_O4aJOf9gvAH9cfaSI7cwgYPBe1ckN_1Mx_JTasK6yqHXwkh9b81X3-ASpbFyhawT0VRqE5Wjzmo-XSM41AuEeMdhijw46V0wdAWXyGNz748BFeMJVkh_JHVLob-l5PTy33lW4",
        "https://lh3.googleusercontent.com/-hJxtW4__AMDpUdh8t3iqx5AC-FoXXrjLt5nTGDSR4KDj0KrBoFXS9vwZCIv4KciSLQARZHD1zx5WsH0_PkyYvkIo9G6YA6Y_6-5nkQH2c-4PKRf9o2Z5F6rr1HjfH0oVNs0yOs1xUU",
        "https://lh3.googleusercontent.com/HueCxFHzs23G5KjtM5JTgRjlU1TGTe0NNnEa8_3P3pi1eWLp9r3nB36ukkip2u1w2AWc0d3QD7zwTIsbwU3vYTEl4_eB3h_4QwTkw6oll9l36bgYNQ7dwPjcutqv1tmwUtEJ1dz3myQ",
        "https://lh3.googleusercontent.com/5DNtOjzygq8gzN4zrODXOx5DKHocxb7bzTQek822RB0sr2Rs60nooqG0pQA-3LstjpBPatFQj4U_iTHLBOXZcGwWDZAcMLncJjE03Ak2aV0ACj3tqdw74Mn5R_Aigqh4yXEszBb3TU8",
        "https://lh3.googleusercontent.com/tWn_gYsE61Tvm4fuPV99Omgx4SPlL9zZ7tyclDyiqxJJMfsprKzEEAFfXqstRq3qKT951XcQ5JAmZEaSZc-ve4dCWoViy_-azS3PppvBuVsARVrrWlZl1IbybrQi1kSNRZtYauX3XpM",
        "https://lh3.googleusercontent.com/ZrkaAXBDJ9Efog0SjvA2wvi-YZjmnH7JOkrrQJe_BjxV4gaie5b0PRvuGcUtFemu99qOrlhcK-5uweYVgqq7Qlsy8G5BixPKXVWzXZtkw_yiI7oMZ4bWXs2fP_f2SXNtiDvoyAQUh9E",
        "https://lh3.googleusercontent.com/zW4SwTd06gcDyBOV0fTqV-djxUTEYLBb2_G1PXUk-oGOD0HOutrI3gOwWsyIfsMj51hKqM-jxF3TuaKb6ETqx-ui5nIq_pPaI3SbYAw4Lf7KB0ZULivLIwFvZlm8RK0QMYAbMoR5dZU",
        "https://lh3.googleusercontent.com/nFeN32hagpvpuFecPellUX8xE1FSSpC9SfoP8921E63EHY-gNEP7mZvqKor8rlurKWAlIe9zrtzV9DItlsl5rBMtI3YHLmrhMTpzIiTd2QTIWwm5NW2EmyzfHIeMt-oNu0pEnkjPZn0",
        "https://lh3.googleusercontent.com/eEsRYGfQurCk6MqMG85LOySVJTw8PBgHSHNrlPzVr_4SUvdAXCp_SfTEx-oEBFNj8l9CQ4S-JbqGkn5rm-BrQsACu-OJDM7NllkG1R46OQZUnuDv40_hncz6AzqsFtrqIkTSMBei1L4",
        "https://lh3.googleusercontent.com/nFzXMKAMArZyWAxj5twgWj8EXcNtzbHoy_v1o0wtMztSiE1hLEq8pf89r5k7AnINzQ2EPf5HTBi6Bg0XMYXr8ygyO3eY7mBkSgoQu4ozXrXK7VxcTOnrKFlk5xLaIwU9mUHivbCWSS4",
        "https://lh3.googleusercontent.com/cAEf4bh_sett0PDj64v7c0qZJlnV4RQ9MwIEK-_tw7nxhPwn30M4pNDd0c8wW7lLPG7E57LSj0F76yI_RfHgimQeyFmBtYE9jiHa-71ToJUHltvxRFpZ6iedViShgKUtp3uVXSIPHCo",
        "https://lh3.googleusercontent.com/6A1SIT2JXog959X8tepIxC741hlmbzL67NJsjMpUbpB_8-_n-7yFKUzxplQyeYMz29njgQI4omoaN0aXaf7BC9HJC8Qw80jxQwVxqZEnRzfx-9uauEzemBnVpaj82VYokbyKbF7ea4c",
        "https://lh3.googleusercontent.com/z_g2cMINY8JVDZxdTaAMThpT473nNz8z0LCuenCptZAaRm8yum83ir2yAiL2tLsv3GM7snJXkgDzDWPSzXCDGfFiCLKcK6tA5ONjEByUGpzgi5tajyj4dFLrpEF1AXOcLVYkAg7vIis",
        "https://lh3.googleusercontent.com/JopcOvM81MCvpf_OM9O4tHT4vJk2yaIGYDlHbZQ_wKAlUtQH0Z5XK1aVLtCwNBeP_Xi2C3ijbixOJG78FD5to0DP69llrsMhZB8U-18CKEYu2uE7MhZb6-lxmWwLieIeqtAXV13LvLs",
        "https://lh3.googleusercontent.com/CefNWllFEI8va5WT2Qn7uYftlCBKcEC9a1GVqfmHxVNDXOxZ9JXQaKnWO3w7ncu31pdDrun65BmXiTTTnd2BkXrPbZy4irTEm4cZdvdozOWqonvmFaPFSthdK5nVtfjfG_NFRAfYhlU",
        "https://lh3.googleusercontent.com/j5vc9yltAQXCAp_leromx2gtEyfo6uM0Ks8h1G_ejB242Ykn6MmdWFhSTDFNoyQN4cyr8NqTcRKrHlYWdLuk8x6ZMfaueTrgHlKPGEvHtfev_BseQIegpBM_Ly8TZ2yNCrPmdjDmrFs",
        "https://lh3.googleusercontent.com/6MPQTY9tjFvWyW8zcwFZfBL7-Y7nzrns98t6thim-BQMM1wM0K47Vc8RlLizwTpnK2UgROf9A55tJf1KoQPezUhFgy52GU5mJEXtnlGuZtUq3dR2hB0TiUBec8oN5l4pDNOTVpAQ6mM",
        "https://lh3.googleusercontent.com/xWA0I_TDrAFgpA98oy_9lpTEPZtcIiMIKG-FSeK76F1cY8XMgT8xy5sapjPrWtMQgN0-u7X8M7DJBdKZ1EBvy-tUg2TqaQpaDb9N3PNlCo_74D4PS_pEDAQq66OzjLubnKNgiajt0d8",
        "https://lh3.googleusercontent.com/Y_NX81G5Np8V2ifIsel-SEq5HfgfxuD43vWHHadMTcCaGiRzbeU-KEmM9JU7khSbYI3CmpjMMtWI1UcLaVKrA21mqtIfy1Ze3W9lTd-87XQqgzO-N172mpenbm5dyL0AhEg3lcB2boY",
        "https://lh3.googleusercontent.com/YRLqQz1PLBbc6EdwAXgp8wqUEEG5GWJMq3zefwe_GddZWT-BvchrcyZXowO9lTs09EVH661ndTKrotoWGt5t29GU9LX3ZDsUxlyKcWuvKdmk-4UIKOXU-bPF9ThsZuPxQhTHFoO-dvU",
        "https://lh3.googleusercontent.com/rbN-FK-jzNEHOC1yLMv7hOa7f-cmk6nPULviVgVxjeXe8LVMgs93w6xJaeJmo_B7y97wURoIOJgdDi2HQNRfMBZNHl6ojZI0ZUEDr-fizNUTNONXUho7NWqErJYN_AT9zHbccP7ICn8",
        "https://lh3.googleusercontent.com/9pIGaYr64_DpGfxT2OBvyNKpCrzIcTF-niUJdBBoTVRbrd-pAyH7xUernVtwrVczb5Wso5d42UtFGYWQjHHQXda8Or6VqXpYNRCKOm_NQondGEbJAmhAz662OknE4pghSOcfsO_-OHY",
        "https://lh3.googleusercontent.com/18TwNkb7BHeUTVBBzThBNP0XFPaDiHbCgZKZqe8H1yOjPd7kTqLq_WHUsMN466gl63Wo89c7tG4a8uC7yVSNnhdoFM7uTdttA_lV2xC6FvvLoKNOIkVds3HlfvVuJaiWc9x_B6ZTDEM",
        "https://lh3.googleusercontent.com/YiERsKb9rNYsPRycgGPwL3VNFK39ONxx-Rbde5ST103WpUXvav_da1cOJzH-dx9pymODAnihSZGwkxGbATb8uwC0pk-tqBHi-pbzP8BfF8yjF9S86Xqyl6xdKIS6eGr0EwZihaLyy8U",
        "https://lh3.googleusercontent.com/5UblKfoEfiZnSQ8JginGICuRG4fMsJ2Ux-jnwyVXo7h7k8kS6HjkFGypFPJwCJBlDQbtAHF6qLXLgR7fC2mnmWiJuh8tlzgxDBT-_-noZDX60DlO8Qr1zKDsc9ia9WlQed4qlm-xWmA",
        "https://lh3.googleusercontent.com/O7owpTAn2fttgM8jxGUltu2DNTxh07JeA4k1ZbAcSJ1d5HRBbR34YcFsM0ghL3ptYLwAi60Jb-l6oVLgOEH22v2eii1t-aIDHjF8OYfJRr9t8QVDcr3ADdM3svUGrDUkTp0JToKAE3A",
        "https://lh3.googleusercontent.com/ttHOLX4jYJrJa_vm1shYfHBPFU6uzBv8W-92YsHlgF-_Kh9g67lySfrJCaSwHAjcGm_deHTA6-zEHRmEveA7pXDp76W4kNx6g4R5G0LaYmM9m5LUt2sZtdt4Tj_-aj_DVD6_78ktSEE",
        "https://lh3.googleusercontent.com/jxIvuMhtQalY532V9NnTeSzUJfmb4omMwuM46wl7zA9TGi0Ws8g2q4_v4NN5jLbAdh4tWU_fegQwSKYYbgLrh0BDHd-ZZ6TLHedTQZje1-Fdxbj77uZLVi2XmRNymIVZ34pCNBwF4pU",
        "https://lh3.googleusercontent.com/3a9F4wy50vR1gggVWZk77WQ3eHvUIgaGWuOLkOpMuZNhPBW2ey7F-ok1d77aV_oUVy46T1CemP27on1_uFX4pRwlpnH6v59qHmtICeptdqKjonpB7wZrDlASarrlL6Udtqace4GM1cA",
        "https://lh3.googleusercontent.com/H8wpNz6IzFhoCThMUk-s2gCN97XpwtL3fceCVbU9yfQTMU_KtKegZUHkiS2DFBkQjkcIdJrQAlx4uDpcFF9twtjtLBsDL2KXqXsV5Q472QiE7-SosaWB8vYA7Xr7M7iAvSLlsHtBjfM",
        "https://lh3.googleusercontent.com/2l_0BT-tGo7GCCcNiqZJZbB7iQjXPl-5Wwm6L1vfItlrxatqSiOZfQysIQw-lJMs5a3Oy5_IhdglMo-5HFpQNe3Vru7BwnWRwcP0rnxVKgkIuVzqMWUUKWQPa-tn0Pm3jCKuSobTogA",
        "https://lh3.googleusercontent.com/7ljzPe88IWsZR9hchkAbQxw9KAPinZ-rm2VAaXXJMQY6p-Aan3pVwK95W1Pr1gcSM-2Mzsf3A4j2Di-z-QSJzSpa6WnB9Byee9HgLmHn0taI8jiYoAxbAo1Rk7Lb5HIClmxYeSaWvF4",
        "https://lh3.googleusercontent.com/cnol7EqoVW3GJNGgiRp_RbprHdc7gYlIP8uEDxERyBZIK8_-AhzEFrvTLIUYyfy9wRr-y88Wv2fl_jSbPujviRtp-0mArvnw4qXO6cN0FpzmMg82l6AbPCLZ-vsZMBLtoe_glf1LxCE",
        "https://lh3.googleusercontent.com/3JAg1qgIAPJde9ZRwVhHMHuxnWT3jb6t7K6Nh_z-dJdMhO7_aJI6_AU6uNzhVldv_qGstAhwi5r_s3-5Jl2kvbBJq0W_9RfzTu4GlBWznkWcbiZZGrcHrTtNzuSBi1LeLon86YH7Kgw",
        "https://lh3.googleusercontent.com/fj2Fhw3QCSUo-bW3pUvdJoZ8OBSniT0VsXocwYUvpiYfIJE4oaD0RSNC1Fd84mV5pywhpKT3TQ1Z-TynCXVoXY6u3RE9fN2gmfXZyU0ZqhuuIusV4FW3XdAaFYGF9IaDkbWv4HkqzIE",
        "https://lh3.googleusercontent.com/fzdByQ2A_8kyEWHqFJDIp392Om82Shx1WjpOfHXOqdCJeM0umAzrYnhLl-B-yBB2mPifVA5iKjOVE-LOeiXTVEM4wUFOegB9hcSYB7xRyJTdrLjDsabH6ZksP6tFLkgb6losJz00uCQ",
        "https://lh3.googleusercontent.com/V3O20-bZf8uk-TCA-xznR6wasTfJu0ds5uN0DlKIo9ae50Nqr3BVM2TsXSl-JOnwT0bNX8xKSVEAR4nvc6K8BHDw2TKEeYQr3nJ0AWObpkkQKLohfGhlf6nfuyqqWlkZP16FKAG43d8",
        "https://lh3.googleusercontent.com/DGoocxTA-EbFJL-VzjSyN681nSlBjRja6GaSSSfC-WcMrA1bcUR3xGUAs3dHVpXUoUJt3yQBgtXWBEaJ947eJ4S2hIBfLzEJ2AtmnsmR5z4SmlmukIFnuO8rhkPjwrtGFXDO-n9N8HA",
        "https://lh3.googleusercontent.com/p7oAUNFC7xsGH7t2bzQDThlIcnVHvSl0M3z-61OTD7d0vq9z21FL_TNoGF4xF2DVjvMRbdvr_-o_dagytujOqDGbgDrIIKkTcUUKSN5HYsvqmHL0RCHXA9MER-GqHI0KzA2yHXNjjfk",
        "https://lh3.googleusercontent.com/CxeTqmOjW7EbcKmactuhpBDQCPXuKRx43sJi0D30JUurK41umolkHSlZFOFNbOQDUFBhz70XKG_fagRrR6QaM6Md9JqLDi0R1Ov6tlKAWxhc9nrTwQYFgTcQccqayTZ08Cf7oNSDIiY",
        "https://lh3.googleusercontent.com/DnmR9bQEt1xEmxp1QDiuiprdpiZfG9srTxcP2dEwTeQGmMb_jwdHztperIkzVqJFEWKQNxwoLF9N1FBNdxnk1FHYjS1mmA6d2jIsgiTxb4U-tJ_o0P5jiVF8qlWmZk6TKSpCGB5cQY8",
        "https://lh3.googleusercontent.com/4BFo4hrOvzq49p3qE0MEAvhQT5xxg1PKQ0BvyVoapZc_icWNeTw5Cco8y7vG736McNECAFFFzrBPDH8BWQlZBpeSkwIfiCZwN0ufcxFgPlh7bqpAKn7H5pcwJpj-i84Xf1v_gpBz1iQ",
        "https://lh3.googleusercontent.com/HWy1Mg0H25nOp_lSWG3gVJomrV30kv8VAuAUGqD41lqOgWS7BvQvawgYhsYl3Gzj7EONVDnrEmNvvRCiCJ-dnSD3WwDfBLD7wIP_-uTy40CQPVuXe5GaGjItoICp-UVY3c1txOUYWkg",
        "https://lh3.googleusercontent.com/oXu9ngKLJeC9oNPFtIpERlQm8qQWFYuplJ1zhKu1FxrqHAsbmcagS537hr9khoSxu1mTNmlVjK3XmTxL8azCcImh4-4PbqeeR1ez8l7_KmlIhH_NCfqx-jOGmiDGSAosE7AU_9EYY40",
        "https://lh3.googleusercontent.com/gyB8rH7CNlWjLiw7ula766aNoP7feWPgN2b9O_KAd6ibrtpZlcxnao0SpyvTmGqdUsP411xhS7leGI2OF7j337SPhz2KoptcuWbT61n8PbWOBYZyVUBTaQ8avwxpA8DiAYCrYJrRr-4",
        "https://lh3.googleusercontent.com/twKLvpNh-IQYo6EJ1wUI_5Mj7J9K88PKRF0VZhnr8cXF7-gE7kU5su8DhhJd87Bhd6d_h9KGTcBSyppBb9Gmn10SjmuRbqx4GjmfYthCZYtOwFENnNgVnD7umazKxCQ5q-wKFqqeAqA",
        "https://lh3.googleusercontent.com/aeTKqU3TTzbfc9J3H2xJv6jh02PaSPosknFbL3omK70Ke5chFffwhM1AwRxh-MZO7r5kFCpgBGMGlFjwQk2cut05oWWqtPUBEg5jrzmSARI1txg7W_VZbE3u2L4-2hUyHmHBE04-pIQ",
        "https://lh3.googleusercontent.com/JXqjwdXBd43KFK79rejGcEDNTamtAMND6xykMHh_acRSYP4BgmYu6eYs0Qv2Z0j9JB-4yeYeAcRHR7Nzd5JjKN2OiRc6jAY-CBjn4sMcjUe8g276ros0K_e-1rp8zDbdLqxzXIuuVXw",
        "https://lh3.googleusercontent.com/4XZlWAUZXCLh7Vl9ZO26pd6pi0GTBsiJB_WaZ6UbBuJLLO0uTLwUyQe245vWPXcGYyA8p70y5_UdeosZTniso5w7YAL69LvTZV16qtKdZR11lJTq5rWc2y6bPRYrK7135BJDlqndBNQ",
        "https://lh3.googleusercontent.com/mfX2IgKB6feEMInEpER4W0BEEo5cSKuwoSfCEFPOglZJ1d3T0lBMJa4lAbRcKHVqqf43DS7WESPsqg_XG-1iLYazITzirP7Xsn8ziJa1rjog_FCuzjUHxW4E-s_jkEMEFZbPw7XTEFA",
        "https://lh3.googleusercontent.com/_vPykZIrssyFHqEw_iPB6qTqXgfzP3gHRm5WfVHj2gi13nlxgO2Up1B2vLUMYAi9FDJ3pD_u3hGUxdnBTapP6AHg8z2Dn9le_M55UiQwcbma1FvKcYLrC6hiRMb7a5rmao-atDBO1UA",
        "https://lh3.googleusercontent.com/97IL2beba2J5EVfmZO0Ml2aj--GUhxIK464_rQqSg0NalZBNv3YanvGxVzKmAbq62vtoWJzNhvlL5wq5bCF3O4saJ4GztNJ8wExs_yXhBhfSW97L8I3mwID2Em0sC5z0BhJqyq6NjDM",
        "https://lh3.googleusercontent.com/G2_DkBAXq-k9jGSQCSUZ7cTWsqq2W5H_soUsLr_2CXmpMsa-xlr2U44OwGb3L1d7w2gIeryHFY5KikKqYQv23qXdtBQdCg1nct8RPwNCQyUL402MfA67mKrxBG7mjatWgvAUs-EhqC4",
        "https://lh3.googleusercontent.com/-Dj5Xc2YU7-j5EsyeoyEBR4TSwdUq3KeJhUhkza3xBT79gnQDLw8FNR6VFLMTBtbx2q44DkI_d4-igQHb3Wf4GiQF3Da5ArYTMAuY7GV2F5FnJgEvc9XGmKyqqu8kyjK-ZnCHgwE69U",
        "https://lh3.googleusercontent.com/u2-qQqTWK4Cxx2wNrxIsOxB6JlTNQg3VyaAF0uw8cqDfuKqlA0oSt07dfP9xmqDixEWKQltrWINgO7T7vAszCN3hp5zt8B5dcAAKB4U7szM5GhzZiq0e1Tk6dlEeoJqGrJ4UpCJh5tw",
        "https://lh3.googleusercontent.com/nSqXnxm9XFke4p_Xjp7K0G5Ov6cU6ZLgG8DyqVNP0zZNndbSwtCU6C4eZZPL6OhEYEbBUdudkhNh-7o9RSV6oL6RAjTLSGvMjRx_fHgmrcMumdmxWgwem1yfmU_7G_pwPAAjr54rqSk",
        "https://lh3.googleusercontent.com/57AowpgdeFiJv8yp9aOQBm79sUg4rAU1miA3hE9cADUDyeICYGl1pJzQTsAV0vHzN3V9ST9IH_O4tH9YfBh6AAmvWgkLLe3CIERtqJAr6LLAkO2AQiglVod-JhpckBDo6CemGR9uvF4",
        "https://lh3.googleusercontent.com/KPSaMrY_kqSb-BVX6k-nZnJ_2_e-wkNA_Tx8UC7wiqiwlcuqiUtt7QPieCsPEIZ5LpXIt2WIwF8Pyh6lfDvA-1UetXU-nvnzNPu0-u3R9oaulgIQiLZkV8p_nFeKsrMN-rROK8hPgEg",
        "https://lh3.googleusercontent.com/wfMVlrZEytiOP0sUikNC9t5y1b0XeL_siM8ARYMKxifgUdz7oIq6dEGj6y7RPNrD2MdHv-NylZ7Q_WNgHsTyRKmXQdXLm8_pAT0IVDfcR6Hx2cMQb4Xq4zt45HocSMZenVtNBrmIkI0",
        "https://lh3.googleusercontent.com/QFn9A4jhz3UbiXExDM51saFugvwHMSgLFfdeyolQBbScv3oMSjqVyqkY9rmDm8VhiSrEn1Ibxuf342-t21RrIuz1gMFqxtkNFU8J5gGWE55odpuDvs7bZ0eEWlX-aSD701pG-nUoo-w",
        "https://lh3.googleusercontent.com/XHljymfymI34gWClbWzUVIZM3JL7O5c-bGWuVQTu1iYa5fOLi3JkeG0EGHFOkv5CV6EaAsw_OUa0RDI0S0WKmkDJzYFwLgY3xhYiM9e7wzGFI0WDAEuQIKY-V2PqGhdGZ1XLniTYb00",
        "https://lh3.googleusercontent.com/ca17KbQSqgfK0FvScA1QxEvX-fSiP7kLtReHLYbtqbfO5L79zncB2H6aUi-cPOQGt7S1gMKhUkO5n1qoGGIB2tq6aiFiIXOz0WvL-6B0ygNsD_D7RnSRW92u6wdN1sHNDdu29hkXTCo",
        "https://lh3.googleusercontent.com/jwugEXu-PuUfYvAIoXcvZCLZrX9K911wiO4s1SJV6R_vUiSt80ugoNH2HJzrlhnZ_f9jTofOgKgN1munNyKpTAdvjSK-eV1qzCGSYF75li1bwDGWyBvFtzSKu-gZh8Dpde0bopn7FL8",
        "https://lh3.googleusercontent.com/DX5nojRVH7um6BT75AT3kxZO_Q4sCcLCEXqMtzq9SkQBErZaQMRlxW7KmgIz0UXcBLAeMoe4I8y85rUTPhH6T7E8Udxxh6FuDWjlb6Q_zzcmokLhLFwqymMg0XUyUPF8wUcCcS1tE58",
        "https://lh3.googleusercontent.com/uhhR8jGbci4SrWOr6RiFP7qeZPKcaeZ8ILazINwtNjP14JR3oVZL-Iw__3m3PjGQW6FrUFK-Ta0f4dEssSEIDB4dfwgRdX18UmWy9YVADaZOco3VNB7lV906XURH91L6y99RrL1ByNI",
        "https://lh3.googleusercontent.com/qsP5smQqqCf-Fr0bhoUzMxfhsZf4HV1qUk72I9UyVQA7ULHUuUfui5fsFhBJ5OxaYBfVo7PyAA5AfcRh7pb5naIl0TZugT4pCK00fH2mMB6auVm8F6NYnsdVWTYIBzck34rC_ZtObMM",
        "https://lh3.googleusercontent.com/16H3-Oq6jPKNmo4SwIluayFAifMcsC31ggPFZN8_QkatkKKZkzKP3Bi8l3bgwHGui082G2E_6La6yRM6Oe-Zwa7gHHvT-ViR2rf1IJTTBfp3W65h3OOgHwGfhK8OwrpRfVEqubqT0Ik",
        "https://lh3.googleusercontent.com/_XIDPRUaUjMiVwNXrThF184kx8AjRqv-iSgI8vfzekKQZLp1DmMT9OV4rTOl3oeBKmDYwXpL-pHFz3_wambo5gGUtTQIMBiKpkbHRrzZ_Cx8SNptMVER1ijoGq6I-2EZXSy2jdOaRw8",
        "https://lh3.googleusercontent.com/8cS84i_76tUr91IPhH0Vd_zVgyXvkO9FV06CCVUsWCuT1UgorZL348pX0Vy7JPW2VkAsa8ttQDEPyh6Y3B8sNT7GoLG1JoSfluIB_sXhbY7spketH-pBwkXvzffSkdPu7xuuYUbEtq0",
        "https://lh3.googleusercontent.com/uZMYZ8WnRi_ihWk8bGhx6cyoMXI1jjCK6_BUuFXD3xKMQKC4TnlTpPPDvJU1X36OzN6i1HMVQ08IYHDSTWZqGI63j8P0IQeV_3LNHSIFd-FqdTHc5RoV3QUFy6u6L4Yx7Hq95bN3rM8",
        "https://lh3.googleusercontent.com/m50P58CrChkN0rx07w_hpkuiksAFssjlxfOKhVWabaYg4YQnQavGfVv_wElotCq2-MOrLe8f1Ylmmi-5fFyhUxe85PYmutTpclN_SoPWZTGRz10D-m7ZKEOij7NGcoOR4t6SC-3c_eY",
        "https://lh3.googleusercontent.com/6CIjlnYVSOcUPhU_BML-yOVbu5ns2AKKelROcE9VX7rmR6grwDA0l69GCaGLpiC_Pt-4MWMEMToiQ5nP0CeHMoeaPKx-sEiSlOYd4_U5gUAASxQbnHv-Z8SV4ZCRq0R4c6Wja3aktyk",
        "https://lh3.googleusercontent.com/27_XrfH2gS69EWFEP5Y9R9ZETw7f14trIadjSFC4-DZTMcgVYLWDu99DYpkBgUOo7_7-na_TnJJhLzCS-HMS-G8TxJg8dUu2UBOLbTpg7vwmttGompZ2j5JREbwWjCgfEwRHXkVViAM",
        "https://lh3.googleusercontent.com/fDAhsnQy6RgYXZQkg0Tfzxf-7VI_LpE5Blpiyfrvg1F0fM3LrXFJtfQpVGSmMft1B9kE6MYjRgsqgANaB6npjCJtcMgMPfAEEmiRUUQZ5qUICL28LDez5A9gsb4d7Ry0LESGaUfng48",
        "https://lh3.googleusercontent.com/lU-eEIiOaJiyWPw6jugqKxv2SlbHpphTC5Gk6PetNcKWXdXgU4kED1bl1cZIwS9ZAPQ_y6v5jSJVg_TiSANO_wwBbAOhiIIRmppsijvlVh6M3rmaumvFcRn6P91pB0C3l3NdciYwD3Q",
        "https://lh3.googleusercontent.com/KNj4lzDmXtpeSD6TMLwAefz7qR7jLb76Oh9TzH9Xx-ir0Ufny726tzItAU611lPPtHzeAomCZo1_SyJpm1bXbaYykOBA-JTciD4YJGi1x-ywFLQcawGHgS4x6kG1nkH_3Ku6gmf0S-U",
        "https://lh3.googleusercontent.com/C5ViMbsGQCj4vMiqQeWpN7Z3tmYSZnH8fVWrY_bN7a4F3gdtJYGNHDR11Rucm2S3FbQjKW3lSOXwLaz0YzSxgvtCrWKM0NWySqXJWyQti1_YKY75o1P5ELHR18iKFvm17iRkyVzHC8E",
        "https://lh3.googleusercontent.com/t8bcTRTYT8c1-YphE_-tM3qhIgwwkAZi0svr4Rf6JkpeO88rfOcWjSNNr3Xqu9xFF-Sltdx8V_GjAelQg9NLBj245LJ8PHLizNGWuho2UdAJRSQjZFc6mCJx4Q9rHwaEYgJUZWQTrwU",
        "https://lh3.googleusercontent.com/dtyqJExkias9mM_8Zo4OL1F7ZWL7up6MrwUGC675lszbul7-3_WAjHQmx3ipfxlX5El6UehCil399HV7-ssMS5PSNCmU2n6_LTVB5QF8f6-caeY9-t5Lg5zfLcNyXV85P1aF_reStOs",
        "https://lh3.googleusercontent.com/Q1O2O07-zBj4ZTDNol11hBQU7Hxb2TiOQ1k9_K-FfMFJXdC47FkvjcTqZtV_ZA9JHaZ5e5-rZ2zibMQFS_qNODAztgWYEovifIvNp5LGt-4lz1nfU5ol2xUQ98H_bJ84zbwobTlffaM",
        "https://lh3.googleusercontent.com/oG56nVVCVHqVsAeE9JRaKeb7XSacGxnmovJhlfndsagBytketNrp5z_fESWbImm69SmTEn6Mp6Rb5M9Z0IqEyv0qesnxKBYZ7xQXHC701v40ZbBtwvvvc1dbfyKw8CKMscaWsC4vzXM",
        "https://lh3.googleusercontent.com/6poHuSDg7Dh6Nvrhg0IWeDVrZiGkha7ONNH7iVJ9epKOy578J47JuPjPbqf1o1N4qRanIth4_aq_RV_2A9xdSQuhH1V9dhl_QdwKnVGeE7ZwdadLdfkpk0EbZyGTBP1_C2tLziMXJiw",
        "https://lh3.googleusercontent.com/8clk5HsGS9vU7CrHYrjyF3UYzxtLR9Nc6EYLWohnelXqC2jFluXieGWuSzK4M7q0Z36mO-xT6vQgX_ZJg8WTxvbm5P6DlYU5Pcra_UMwwu-fro9CnVO-e40QWcMLS9Je3kodWvxJIhE",
        "https://lh3.googleusercontent.com/_8gwi0gA2L2USN-b8KzuPA_Fv29i42IlDGg3XZNmp0xaZ9c26zUk3s18NQoDPYud8iNtjY8o2N8Ao0P4IOKu2wi59JZQfnu_ZZY2xsMjU69iZkOJxsTR_TJNGPZU2FfjIy2EMRMx26A",
        "https://lh3.googleusercontent.com/I1O3mEOiDM8OVy9KJAA-PIjcyf5gw0sDqREsGWVOhwnRBiG_GiIVXLsWMMteLNp0HuuP-ldEiiMq2CpftVduo1Ri_2ecIgWnjcL95277Hf3Dlb6ZaJznDmaSfqn6HL1eI2rUG5ChjAw",
        "https://lh3.googleusercontent.com/ffUi0WlNasYYP3D_7XmffKTePdKbPAH1KA3hodUVBL2jAM0RhZTffx_O1fZDwDjVHplJmkEYb5WvbUgzCkwdTDl_KPFFkQtTcu9i0zs5U9Z5pfk5uFNxlKDLtEdUV434Pvyjp2PKja4",
        "https://lh3.googleusercontent.com/OtllLCMD5n1qMJgqnq0FNJs5tybQs7-xpj0x395pRLvd_StO-DNII6T2tqrLfKwfIfdGBzGOwR9Qj0qLF8w96yAqrZSgA0Tqyk36EyQdM5IYx4PoK8_7E8PRPoSIirGg45MhP9F-ASU",
        "https://lh3.googleusercontent.com/HKNOHYMrt_b6V_jPRYGJYQqkMlqUW8PlN9UsQAbXqeaHWYbl6TR5u6RaVjECqyoBMSiErCqnac-AwV49jJ_yqShqhG5hnh8URyQTw6a2lmhSxHmTNMqDLH-X7poUjC4t6gOhMlCQz8w",
        "https://lh3.googleusercontent.com/i2SFaow1fMk1SkfVkG8WyjY_L9v1nnV9oGz4OD5KsjJk41U7oBfbn_wQtIVowHn5uQKwYKg-kY6gn423bhHxfWGIADLP9mI4rGrKBYDJaSMpDTGlbtNny8VBSRp_ngIy75OoB2CEaL4",
        "https://lh3.googleusercontent.com/W12IiIWsfrJMUblG0okE9NtWXa66VOz6W5INxkXk20T6KHBZBTmMjdymRZZ-IhbzWHMWnZq5kK_DHraXu1C5EdR6eVxh2xxpBn7wasaRxWoVgqAqpEP2eLnpxaSs90KiaMHjDgN8y2Q",
        "https://lh3.googleusercontent.com/B4vToG5aARCzzF1SF140lS5-QDsc47tkechShbv2YB0oinWTXMOGAA9N0lKi-GXQFPIpsKF0YkJbfkmuBUDEXD4978_cVKhfA48jw8-jiTntlhxPfRGiDo6eE7i2FpQFF5J1UF_XmwE",
        "https://lh3.googleusercontent.com/8-V3FrIg8N1vjFxi-MUsa36EHaFkSSaWDjlWAa_F8vjla2Vjgvs3hISIwfGq4kP-7cRgbWOLsm27vXMKuvF_xk72Valmpux6nW3w3o22QFDxR9tTkiuT8d7MCakePdqGSkSSNzS7IU8",
        "https://lh3.googleusercontent.com/RHKfYG_bnA9WSUNBiq-Mmr8MfJyMXUpI7N5NCJTvriNjusIJNt2eUp_NkvYtJHcMeihizOOgHPOjpnF2cT_zxIuJx9o9bynQJOeiZi314mE6XIEdtDehMKOUAJyPj-rfQz0CXjd2tWs",
        "https://lh3.googleusercontent.com/OtMXZ2Tewa7IDSWv_MDfFBql4DDwDrGuntlq3IDOpAF2wYg3JSm3f8OlrsIV9-mMq3qpserXNG-WNeU25IAKp5AgERhtw0r8RxCxN0Rise9rk3_40cnC5r5LH-0dvt1yAtYeAFNGe6Y",
        "https://lh3.googleusercontent.com/fdUf6g30ZYBD_lHYTzIxGXKRrx4VsqoylnCLJOsHQ-BtAdE8uOjS3y6SSu0W3hLu1-0A1ZzDdVNTLReozu3065KBIneZS6gOyEE4-TN5nwjrwXG-fOgTxhtMMe8NvJgM7Ye9HFa7LCw",
        "https://lh3.googleusercontent.com/SpT9UFE7Wg0wYLY9wOpS1ZsbQ-6_19mVdYwjpQBIkx0UK88sSTlZxJ0voINMknzc4uj6qd4MdgQCxiXrrcXppzv29Lx5r092DztMP9jj9-G8mn7RerbvWlW_7Cfrz5Y2FdmhoX-Jeak",
        "https://lh3.googleusercontent.com/4NfAhm0bBPsIjqcOXQRf50VMecsG3S8ehRYs1tlwY2TL9dNd8f2ReXDUAI-KwsVVROS-nASkINZdcJhyTpJ5AQvR6rNnPGn3n7EaRGOYpPCei8UPIHB6Ktj0tCubgZb1DiBoo4cvqHU",
        "https://lh3.googleusercontent.com/77IYORFK3rxUesZR9sNmQ2zzjYtUbun6qrOd6l81yBFI8dyadRULA6RTKImInrkG6kyAjFFCcNVTl0_VnsS5Oz252pzsMRZoeJiQvd-Bv1gVE7uKx2XxC3nQk15E58A-Z8gteF4gbIc",
        "https://lh3.googleusercontent.com/9fLvG2S_WlEwNXvst92Osx3A7gn29z8Bxq_Hl9PkwTnLQ4Z3QY0914p-JBpr1Al-ibRydTL3m5mWtR4pNv5Mr8de6OBlV2C0-G3p-M_e6srl8EphM9dXi5JRFrRqfHkkM-rzTYvSpi0",
        "https://lh3.googleusercontent.com/INg_6WzeDz6uwernT2fdqgJaBMWGVjVlbPYOA_B9n9E92OsvvDSW-vXleqezzIko4JSLrjUs8Echut_MqR_t_xFw53BRmrVUesfneIYB1OLA-z1YJlsTJUqRk-YNxyV9jnb7ZoktP8o",
        "https://lh3.googleusercontent.com/ADyufXZUrULjMaGMvrAmw4frNuhOy1kqwESGkppJzzuNepCVfEuO3zeq_B1kwzP2FTRecOOzLC3HtNDuF-p57VPeB16IExnCudwvuxW6DXU4ht5_i6h7FFWP9wZRm8jQbKbwtw8F2S8",
        "https://lh3.googleusercontent.com/r1prBZklcowFxpoqJWGQYiyhmNTzL7V9rwWdVNCvNZ82bO4o4umFE8vM9-ik70ZQf1CE6opphOPiPJOyxYksEIn86V_YK-Qghx-PRO6IT96NFELwitMefaP618uZKKzgcoqa_nVIXO0",
        "https://lh3.googleusercontent.com/iaQRlLFlksu3JxDMRPsEUTuGt4X8VfcXO-VO8D2bnxorCSWXCBPeySl6pEMBdf3D1TEy3Wckha33rXp5qlLbW9XtuZUdvXuxC8GlWEGhBIEYkcufN_7ylpi1gTRFP8Tsams626WYyoU",
        "https://lh3.googleusercontent.com/Aomm1SJK4Iem-R7962Opy4mcer5ZX5qEc8taxkq65kD9jQea0y3Yzmlvd2YevSn9Wm7I9GpfAuQlqvqkzMcp5MQBh-fHdZR2pI_8CM4_Yx5UJFJFRybRzv9XK2MooW3tmePaOYFX9k4",
        "https://lh3.googleusercontent.com/-meOLbfTM0wymiA2vsMhSPAWGoKl6-c73LI_-SIFJHeZU3kcXVdTH1NLM1eqo2_NpnFadqKUsq6j2MD2DaWeY45cMyR5KqOIvpvcIXV5uwZ365hCr6PBE7pA6DXiXYnZJ8w48o3Apgw",
        "https://lh3.googleusercontent.com/1vSJEkuO4YvzsBZww9YmUZyicJQdgh06O283qmc1zQzRIAXRckXXygA4XlJO7S-zlH92mk-S1vhjkch9ptfc11TMnSr0Fp64uq6bNlosJ0TqmkF-iI4ihtRcV_vNjrqJuXxwkexOFQ0",
        "https://lh3.googleusercontent.com/8n7sTdcMbIoudfF7nAhUqA-qAfDRgrAcFiayRTBww--EZMAqtM18VtyGKV_E0yvJdDfIkgPsB2jzsHonSSPXEEJgliWayIOtXk5dzbs5qFyJZaF-9dvh9zRqj2x-XhP7j8yNP8xcfU0",
        "https://lh3.googleusercontent.com/EFM7NifQedy6hL2FYnn6tEJ8Zbs0mOTxLbyZCC_nM_rKmBGj-J7I0GG1eYji1ytg3vI-77R054JZdzQVPIDiq9ptgNIb78L5C7YC_JI53BoA3xww0iYQ832amziQWjYHdaJBNca8rSw",
        "https://lh3.googleusercontent.com/Gd5QgbphUcdBNXtc3ciUxvjKnFQ7r6-Y6os6gNLCaOZ7fhqFg6JNUm65veWoOkGCGx-U9DI2MkAcBVqvYvFvDRVrugmSw8UCU7NOs7hbj1uXYQ1B-XGuC4A6Fy_MQl1h8IMZo9_C4BI",
        "https://lh3.googleusercontent.com/kDHzuv3GBTTfMldKLxboKudGeM8Iw7e18wWF1RdjVrhvvXVbfYF5qD5C305uM4J3sp6r3HkbRiasVgEqWeGwH8jKIIRMiNkOTR4hfuEJsdfyVCn0V1Hppty86_2xQFNa1fJrr2NHC0o",
        "https://lh3.googleusercontent.com/2h0Txp3gxkCfo1YSvL1eYFGD_1eqqLxLMCoakNpIxQk6qltNFYXRzQugH8tOrLQo6voK0YhX1nxCBbLE0fJvLfgTOtcWDFDO5YUuPz7LvJut3wrOhIJLBNBdJR73VFSms6lSNuwIthQ",
        "https://lh3.googleusercontent.com/CNHdtW_9wtPSXcldleCiHFnmkHH5_1exIlvd7T28SwnpTbbvfH0ntQVh7PuAXOqXz7z0MnKsvseLe3raveYlR_4U_WK9R5lxgFFHu5MM0kYZFiwHgfHAYB7tNCG_VBravBiRSMNzn3s",
        "https://lh3.googleusercontent.com/yZP6bhmVf7ZslnxnCpeC8ptafsEQ-zxVm7QazOu4gIh96W98QJyr01TAjs3qnMo8abA0x2dpPhyRS3JxT1mXXOqp3mzl4EOSu53T74jkkUvznDx9CAzc1J4oVgPbHhbvQlxzQ-L6AyI",
        "https://lh3.googleusercontent.com/vjqjb0mci_lhK8TfH77z7dusHg4Y7SInbviKWieelqwI2xXpQdqJhHznl53WKcJItGyvjaL9BafVFdgvVmTmeh9N0m5i3fW-1o22_y5NMS3kPIRp1Z3c4Y0wjRZX5LpFFmbwmh79OyQ",
        "https://lh3.googleusercontent.com/6Y0Wy7YisJfGumHEEUSxepLpvcH0ThcjWPQRzN1K8rIEBqXccuIiRwi3audjCQOF8ICrf6e90pcfp2O3891tKf0DvYypXH5U6QC3D2bTpkXicu3X_GKXzni3i_AOPA_GfQJsoqJ6IrU",
        "https://lh3.googleusercontent.com/Cx_Ty83FL0le_9vTGZYIQ-HF32w0dtox-OS0mvMJLloue4IIxm9MSvtAkLJnX-ZNWUz0d_BqN57JZuXA7ArnAwbQpqf-q9_Fhe6yimJr700g6hUn2GGje9w4LBd_dcwSv3Zw0A1pd6k",
        "https://lh3.googleusercontent.com/OUzchns10LECIFAz6tOAaa_oZ0JAnhaeTYAPsrLbMB8bqXvpjPVUn564iiNRGCA5rUaZhreOC-SmoKKDgTVP3EivbhIrIlGwiYPadveHmCSnE6vXWpn4lkDZQj0_ObHYzbPktWTGe78",
        "https://lh3.googleusercontent.com/2HgI8mcliLyNOyfsOUQqQiD-s3W0iXgoTpFxp31C5la6ByBJmxlLYiLT6AK1jZh1JJ5T_nutRskN3atCS5mseUwNil1sbW0WW9yU-RCmNl-fjyMuNg_rh38N94rnMGSkX91y709nZi4",
        "https://lh3.googleusercontent.com/X63BJkaJkY9hoIbczbGm5JviYuRPMWVlPTGDLbprcqZYeadEQIsdgyBn7KdKU3NY2yFldf--5vetgVP61SA8Jvr0EOlxUDuWcl8fUIbJZZy5hSLcaMQZFJe2wL0LO3uY9gCHS-9rnMc",
        "https://lh3.googleusercontent.com/oKN5eKpTr1xHxCjWlJyHsECNl1MgA3M8g7aF_rxDXTvYXR7Mh0BnN7Zq8f1MZ4gsSZBXrAER_bX-7dNb7UEFr5Q2TqHkEwSh5d5PWn3JssQ7wKT29WobbvqTsvgt3xQkqEgt_kC2I3E",
        "https://lh3.googleusercontent.com/wyl5qjEwYViITpkhFdD6QGl4r61hPgF1cBMS9j-NOZGr00EH6N4JtzkGwxVjB6F7Fj45G5lwnoP-Z60cmbUYF9xQz8pUfOhLaQP4ae-jpHssQWdXbBlHv_UUZZKv3aOaL1Zvdo8f2C8",
        "https://lh3.googleusercontent.com/8QG2M0zRnTuag6iqKVtxQTSTtzau726V8P95J-oao-ID85Wr8wSeyYCJeS5aUdsWht4nVUiGTz6bQTXfO54hW0PgFWchVce8XvOvNZBocxNWGOcZHmYzV49wMeiTJ7gt5evNPFB30f4",
        "https://lh3.googleusercontent.com/E8McRxBNIluy-_-eQSwCYV9GoFyeUcLU6PPIgkJocG7BNPZiUNz53hP5rug2BrtASLW5YAGQ1npdRyrtUEOBO89Q_rPCu29SvYfADCLpPgRwqZ7HcpxGXy7rZZxEc_amXuFHpFQUCvc",
        "https://lh3.googleusercontent.com/obh-HcQJW8LLLGoCepQh4f7mysrUAM-GY67ngtwsSs2lsLFStWAYuRj2aWLDXZLMt9Imxuzo0ryivt1pc5ywPvoUFTRTYcJKLsU5XkPXNPwRXMqNVsXywUVv5xDDqAMxKxAtdtIOrGY",
        "https://lh3.googleusercontent.com/KCw5tLWfM6REkQ7QOmokf-z_uqUqHbUjQGTQl8TjnFZ68PmAuq0IK4h8U9d5xGTj7mLorr-jA2-T5ZqV_cV17-MJVGi4ze6EqZ3qDCtbTLOdtvKSEowNv6MX7XHQ_9TeO_IQPnn3sqc",
        "https://lh3.googleusercontent.com/wPR3rva3MZNz1QrtSAkyyvGAarHWV3sfjXFE7N5ALuMJXVtFPjxraoteqBtQyBeddop8JWfkcrDeYNNuCJSAkjWsKbx_q06w41IJewcevXX5m2UGcm7ljJmDv5HmLlYVpzcYiA1ZXVA",
        "https://lh3.googleusercontent.com/U4xoqCFOcfoGZEg5d-zeFETKZFWTn8LXzTri0kbqh0JxoSrDj6NH4TdJY3XV5tR2DEPJBuff6OvctE-TurucIwvosJyIjcLVawfnmcjUxR_6n21vhSQ6ClePNv999nzImK2SLMKqtPI",
        "https://lh3.googleusercontent.com/m8W32j3m5SxGNJkllpesOd2Js_BhqSxxM8rfZcjLz4MD147pTSY9WKkvjAkuJd_8q5UUxwn7jxqspt730jzPkpz8usmt-k3U3kf-R2Vv--nTL8SZL5ESP3uGUnVfSztQdgTzvMrTyAg",
        "https://lh3.googleusercontent.com/m6FC0uASxaZrUFI1ZqtUyBWAJVzs4_P-xSu2ZuLDuwqexDCYxDC47MNBQMdKixoMex6kIaK8Nl5XQgVEauHDw8e-SO5w4Mh9XD7LoQBoPYY66PqQuecsE5Nx5r9hgWS0TvLSgkxk9NM",
        "https://lh3.googleusercontent.com/mkYdo97CtH8RtPoecooT-4BxlN4Tchlx8vvK5IvQT7mAzVXZRPtgMLJ_LXXUAzbcpQCaAHPeBPgi8j-4jlYcYB_L6BKhbi4BfUGEATiiu8LSdZVC4azV8wHKYNq3bSaRU3HbsV5TiDA",
        "https://lh3.googleusercontent.com/-SpYpiQl0WwMUk7MG3tXAwcbub0g8PT6Idx7M5TeCxueJXsa63LFuAnLD3Hd-FecQ-oxLJmhCirCmmND2AbW9bW2M03Cmc3tejYYHNksKloAVzt-vhnY9jL0_6xfD-3P-pnR_l8yeTA",
        "https://lh3.googleusercontent.com/esRS37C1-AQi2z_L_36yNgJVS_1zOQ5-UUZxbfTvQgixEAOR7aGDyjZ7ySCA039mMi5cEX0nve5i8pyRJ8talW-QF6vT9ex4ZAoxDpY2fUlteddadQJPEHHyvEPH2EQA9Gwx-fs3dMI",
        "https://lh3.googleusercontent.com/sBbT4xcR3w5qWDCRgSY8mg3FrR95VFQB-KXAFxgIQiuQmAP9R-M1vSoxxhiB0qiCFRWgpK41-P6_dbEeOJpTBwYJrNXGLhXAXifp24r4pM-2w1G6gwSRtAaQU436LrTkQMnvojCGzMc",
        "https://lh3.googleusercontent.com/5X0zgjqb8SB0bUBkoWSsWj1Rn96BOeWhTlXX9FvdcJoD0XkudYFZZRwYACn1TdMTJ2PLh8y5rtbOt5F5TAae5iHZ6IW99O1XSPpwZ_XVZ7MjJ8Raplqd7UUPepVzU6oqKhHrnT5SZz0",
        "https://lh3.googleusercontent.com/W75EE0tLhZ8a6S3WL7Y4cgDjvcy3MNtOFxPNwHalnIuv0UlK5hCENtHhfk8p-P_zA0PH4nop-pKn4npYveIlI5fKrN6ztIP5FxYxX-DAf-5q7z-6y6uDkT_dBJ3rLOcmTnJ6Z0K9GN0",
        "https://lh3.googleusercontent.com/lZNA8MD988BlfN6H9GVJQost0CByqoSRsJKXilL6bFxLXKLawLRtwQVIEDEoLpELKEkocFgBtkUmtISM7Wr7QerXBglJIIRIsmteDYcj1UjnYF6j33da_FxHURI6v30m1eIfJYIRwKo",
        "https://lh3.googleusercontent.com/Hjq16ZORPIjjUNyAflJ-WYEbGej0gWmyqxpHNMwWbtHkPRdmaXmNoUPjI0TnX6eWDNblvYXxfgYACJRIRcVebCG2ZkN46J10d-YX2pJ7Rf63BZgJZtwuB2StLIaaFeHXIhEXdQ3DyLg",
        "https://lh3.googleusercontent.com/2MkkxihuoeeJ72Lilj9M1Ge8Ec9EQnIsBEgg-sDMy1q5Eyj-E4tk-N-gobhdGz-Dto7CVYbMwjvFj0fX6PGfqp3rL11ry1yUwtiNRmdM_58RoQEmI0cbwQHeew92smyro0fHEAnFTjQ",
        "https://lh3.googleusercontent.com/6l4ItBQ-fBnjumKIcY3CpdA-2X2tv-SEt5jAnsicRQQ3fWGj0GVjWh9PIkGk4M80-W7O7k7ftff2ihTKDBbp950J0ii6-OcHXtH6C4-PhK8QC-AMDbUGFTrzTcS2CoYpYUv4RW848PM",
        "https://lh3.googleusercontent.com/aRgF7rP_gcsG7Kt_Ag0ZqvAaOJDkB3WQwBnvLS1YH_Z19UBLDu2RhdiiUaXZnb5rqGPNOgnGDfRiX2Hm7nm-HhJAvyjex60x0rnQhoHzRQlajbpMuv9ouxsHnIl9KuX863btSfzhFTQ",
        "https://lh3.googleusercontent.com/GDFsXUT21K5dLCj9BrVoOV2WF7rJqaMdZXUy-wjN_fMNNiBIsgqRi7OpxV_VX_bx-apLWqDLY1MpkVCEEVLyHS0I9b4h_mZFd9EIS2b6Q1GmFbnmGoVRR3M3bqFBecc3W7c8I9ZqoyI",
        "https://lh3.googleusercontent.com/mz5gdlEK2FaXO5HYoUNX6fpumN-Xh7HsvIAxJCc5EtrXWNX5LzbLGQNipDJqlTkbQ_dSUvGSoZWxmpq-J5iQcOmM6uXdFiaXEDcNZLBeiqaiqb6E2fX1-Y5EcwGTFBT9D9oR4SMh3_M",
        "https://lh3.googleusercontent.com/_YQAkHh8ZoC8-zuyBDEShRwmodHjPbRpVsnmgJ8JWTMjH_OfYiKKyHOmKM5OOYk-OjCEgkrHNVlND9WfFiQxv_7MWwNPScWuwvQvNEa_Y3OB8rXmkaRIpn_hdNYhLf5XdWOijn_S-1U",
        "https://lh3.googleusercontent.com/Cn7Xtp5SUe5m51fS6BaDpp5MsHweVqo43s6QAWqrQp8Qy7sH2v3dpn571-PmT53bgHh9rUj7hdd-f6M_TDNRTnyrzVtcAVQFg1E81w5iWk57V38QEDuXJRjA1sVrt8buzTuPB9lqJGQ",
        "https://lh3.googleusercontent.com/kCNPBsAaozc_5OKND6pjwmFjj5HCUV8VQLQBDYthuDeO22H9qlF0eJsrIv-jtpgnbtFbenjlLeP9XBQyd5LbRU_2NXl35Q2sntdTK3cdP751U5hGgITuo7PcwKMtuk5FGdd-Lu6-kc4",
        "https://lh3.googleusercontent.com/bvpyi0cTrzoMj-k5JBqSWpr-TbT4j86XXNyd2cdX28RO_x34_BZPax5bjOYMB6XpMbJp59uQD8NS5XoU_onCtQ_wcuBbKQcpxX6M1Zg-e-zJqfXaDNBqwSq3ZbjoascfMRkbjWV76-4",
        "https://lh3.googleusercontent.com/ojkKAdm3uQ0J1G2XGmCz-P2HVV9S9mjCwpxBufN6rJrDQvbOPGpMhIPBaxw_fjhsezteYeNiINEY_e1a6QcZrB-aO3gX6L-dA2QkqgiKqju-qDPmaRVqJGaKC9Z2zn0gY4YROmzCg-0",
        "https://lh3.googleusercontent.com/ZG1C0ggo4lf1wYPpErKiWuEoZyiQZT8UQu9DrVmq3ewscoAHv27RcBJAaRz1zXjWZPWs0hPjzwFR3BhV5sSWFzpCg9ECfq_i9M3uGBekgME0Bzmf59btUXcMOh2J7_FmFN5-zYfpYFU",
        "https://lh3.googleusercontent.com/zpKqrR_3-op151HqpdF-Gi0--jBlxSx23WKbGVyj4jUnXSRha5HDZa1I3ySnpxdkGQc9t_bUAOpGhczRBI9xHKyMt2K0mASfhjSzm8BSdq4xFsF7tanWZDRWIfG592-6D_EDI96UW0g",
        "https://lh3.googleusercontent.com/M0koMPrqxJdwJOpVo-g1ZA5f9NSICiTcM275dhsumSPAR2X5EcBNpYSc9R57rRCAwMBp3t_Q1HUE_YhStFY6hWgteh9OtdkjkCajJiMNyMqQ7O4bLQNzBtBmazVfoU5tvTBt4uv7-E4",
        "https://lh3.googleusercontent.com/jbQpeGnaMCpVu4CMkzaBdPfls27QvEIJuWaoQmGfduz3i_rQZ43UJ6jt8lGW2TtsfHOELG405jVeP30W3xhQ4aQa0SdyuI2lEP6eKZZpnYNHlTpIDfcYhssRGG0A2sWHfeP8FfsYYuo",
        "https://lh3.googleusercontent.com/3RVLm0X1ni4GJqiMfYWIh7MlemL468veUagRAGSuIfavjm_XTrOL5GkREqdN8MFINFpzfJdZyqtne6HLPm7yK5WJLCGVQZkcGl7GD-74aQ_AuP39PYED28cRZpUlYXPlNznRGkfJhZM",
        "https://lh3.googleusercontent.com/NsaaAkLb_Pnws0mqzjBaoKacpt7UvRiT0nK9PTNbpq3kiY3ERdlwNPEg9h1CWy3i7ZGudY--pPEbjjHc3GhG5V6hyln6yvmERe4wuA8qc87CkfXFabxzFlzvl2gXnmHwRl3NZVvF1r4",
        "https://lh3.googleusercontent.com/1IjJjmR4965bypGI9q6NMi6_10z-_LF8PimwxMsWylURe7bS5-9Z8rM_Fi6wEoKj7wj20i_8ta5BIQcBbU4u9-k87BWuEPaFW2Oio1_cT7nIX7mA3viKKAeGTsVTC7u2x9oedVInPzM",
        "https://lh3.googleusercontent.com/5xYrkyvQDmjyVs3vpOcXVOvSyV7_tHbqxWWcYxs8j2tyBXMIJZ-EoyMlckhYRiH5049owgMqjtkI5DhOmx7wfB4HDxOhbITcLAfkV_E2KjD5Iz-OZgZ8ihzRgS2mWNFhoW3p9tj55SI",
        "https://lh3.googleusercontent.com/elw3yZ2W6rflSoesWFDDAjlvb9NUVRp-SGWfHYmb26vyAEyM3XjFyjwvGkvRVI1zt1f3QV6-rGHwbfanBTkIAhvrlXCXcl3reRNMvn1WvzpjDYI4XikC2I5UK6drWVkoisJQJ02Ivbc",
        "https://lh3.googleusercontent.com/tP5qiRiPr8jHKGkUBxQKzfFK_ces9xfYdbDdeDjyA-fWWew1kRumo6FNYqJQQJf_aQMvy3gqWa5OyKFGEq_vx8NZBhyXXWij2cli19fA50w1QmljJWciiVETyXmSbMcFPadmVlkUdyI",
        "https://lh3.googleusercontent.com/hQuh8F4di5liIBm-s3DgTvraRFTuNML4ei7Nvyl8uGjP4I0sx-I442TE80jS8VvBd0xCYrEALkOu91dkpC7oBXz0As1dJhfo5m3LlCDDd05pihBcONR56zYJcw-tLHcg1lQU1X9KM08",
        "https://lh3.googleusercontent.com/PK25y89IB3XPgikgi0FxxcemUCuX9Nm46AFzijR0X3lCfXdyvN4aOITntfTv9qZzBTl5NDTNXMixWCSSP-3_8yNelsgfUagaZq5PrTUatWiTMQ55N1z_BKTEMI100wtem2aUpx4ss-o",
        "https://lh3.googleusercontent.com/kci8JEZBI9GmfRUIkdu3ZGXlR8ZxaRM8wL8wwZ6c_UobX5AxXtRUbHVUxJiaaDugKEKYChwCRzYmd90mXtP7LquwrXwXSgxfPGgBKcLqlpXGYIOSvm3IwbUyNya-vtQw5i0Rg4fx2Fg",
        "https://lh3.googleusercontent.com/-S5sgFVHbrrdkXD0SYpho4PvDeG8RBTbarhqqG5_hBbC8MW7BwSSCO9TtriF9xDps4i1kq0JuQ_sM3c6Ncv7pB4g-SSeF2izQ4pUvevv8QZlsMSpOY6BK0k2hDeAeQEeUptjP204ru0",
        "https://lh3.googleusercontent.com/ADH1aQwRnOjsWKfkZf1s5HUxbOQomDDlfkYSQO1t3OQEx5fFSDgek4UVFNNagonubfEXdIt30L9aD-y05mSS2J2wOeml9RE7QOiV2c0iyKod3Kr8D77X8Nej2CkCx2KesoT_xoFSHA4",
        "https://lh3.googleusercontent.com/6KfR2jtpVzKc6dTFzceG4JpyqgOpKKbbJh0pGTPRd8ETECfJelQ28Rot4s2hvHQGK6XMHEwdlqLXTrQFDjH4XeR1UpQeDJHcB1BPERz-RX1LC_z82oLd05qEGqwhGNc17_tn0myIKPI",
        "https://lh3.googleusercontent.com/ynxD50wzMAho4s6Z7b3wYXmkv-xNWf_3dmQvN0-6Wmz6cQYMaqk8Vmi6E_KpoYYqP0u_2HsrOaEQ8lhjOXqpYAGmOGovJk1aMT0yhlTFDTNrIsqzAolA21J3vJkO83a4RvVirjA5vWk",

      ],
    }
  },

  methods: {
    FlipRight () {
      const flipbook = this.$refs.flipbook;
      if (flipbook.canFlipRight)flipbook.flipRight();
    }, //end of FlipRight

    FlipLeft () {
      console.log("left")
      const flipbook = this.$refs.flipbook;
      if (flipbook.canFlipLeft)flipbook.flipLeft();
    }, //end of FlipLeft

    ZoomIn () {
      const flipbook = this.$refs.flipbook;
      if (flipbook.canZoomIn)flipbook.zoomIn();
    }, //end of ZoomIn

    ZoomOut () {
      const flipbook = this.$refs.flipbook;
      if (flipbook.canZoomOut)flipbook.zoomOut();
    }, //end of ZoomOut

    GetTouches (event) {
      return event.touches || event.originalEvent.touches;
    }, //end of GetTouches

    HandleTouchStart (event) {
      const firstTouch = getTouches(event)[0];
      this.xDown = firstTouch.clientX;
      this.yDown = firstTouch.clientY;
    }, // end of HandleTouchStart

    HandleTouchMove (event) {
      event.preventDefault();
      if (!this.xDown || !this.yDown) return false;

      const flipbook = this.$refs.flipbook;

      const xUp = event.touches[0].clientX;
      const yUp = event.touches[0].clientY;
    
      const xDiff = this.xDown - xUp;
      const yDiff = this.yDown - yUp;
      
      if ( Math.abs( xDiff ) > Math.abs( yDiff ) ) {/*most significant*/
        if ( xDiff > 0 ) {
          /* left swipe */
          flipbook.flipLeft();
        } else {
          /* right swipe */
          flipbook.flipRight();
        }
      } else {
        if ( yDiff > 0 ) {
          /* up swipe */ 
          flipbook.zoomIn();
        } else {
          /* down swipe */
          flipbook.zoomOut();
        }
      }
      /* reset values */
      this.xDown = null;
      yDiff = null;     
    }, // end of HandleTouchMove

    GoToFullScreen () {
      const elem = document.documentElement;
      if (elem.requestFullscreen) {
        elem.requestFullscreen();
      } else if (elem.webkitRequestFullscreen) { /* Safari */
        elem.webkitRequestFullscreen();
      } else if (elem.msRequestFullscreen) { /* IE11 */
        elem.msRequestFullscreen();
      }
    }, //end of GoToFullScreen
  },

  mounted () {
    window.addEventListener('keydown', event => {
      event.preventDefault();
      this.GoToFullScreen();
      const flipbook = this.$refs.flipbook;
      if ((event.key === "Left" || event.key === "ArrowLeft")) {
        // console.log("left pressed");
        flipbook.flipLeft();
      } else if ((event.key === "Right" || event.key === "ArrowRight")) {
        // console.log("right pressed");
        flipbook.flipRight();
      } else if ((event.key === "Up" || event.key === "ArrowUp")) {
        // console.log("right pressed");
        flipbook.zoomIn();
      } else if ((event.key === "Down" || event.key === "ArrowDown")) {
        // console.log("right pressed");
        flipbook.zoomOut();
      }
    }, true);

    document.addEventListener('touchstart', this.HandleTouchStart, false);
    document.addEventListener('touchmove', this.HandleTouchMove, false);

    alert(`
    Next Picture: Arrow key right or swipe right\n
    Previous Picture: Arrow key left or swipe left\n
    Zoom in: Arrow key up or double tap\n
    Zoom out: Arrow key down or double tap\n
    `);
  },
}
</script>

<style>
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
  overflow: hidden;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #333;
  color: #ccc;
  overflow: hidden;
}
a {
  color: inherit;
}
.action-bar {
  width: 100%;
  height: 30px;
  padding: 10px 0;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 25px;
}
.action-bar .btn {
  font-size: 30px;
  color: #999;
}
.action-bar .btn svg {
  bottom: 0;
}
.action-bar .btn:not(:first-child) {
  margin-left: 10px;
}
.has-mouse .action-bar .btn:hover {
  color: #ccc;
  filter: drop-shadow(1px 1px 5px #000);
  cursor: pointer;
}
.action-bar .btn:active {
  filter: none !important;
}
.action-bar .btn.disabled {
  color: #666;
  pointer-events: none;
}
.action-bar .page-info {
  text-align: center;
  margin: 20px;
}
.flipbook {
  width: 90vw;
  height: calc(100vh - 50px - 40px);
}
.flipbook .viewport {
  width: 90vw;
  height: calc(100vh - 50px - 40px);
}
.flipbook .bounding-box {
  box-shadow: 0 0 20px #000;
}


</style>