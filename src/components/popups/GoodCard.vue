<template>
  <div class="good-popup" v-if="isVisible" @click.self="closeModal()">
    <div class="good-popup__wrapper">
      <button class="close-btn" @click="closeModal()">
        <svg width="14" height="14" viewBox="0 0 14 14" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M3.73341 11.0833L2.91675 10.2667L6.18342 7L2.91675 3.73333L3.73341 2.91667L7.00008 6.18333L10.2667 2.91667L11.0834 3.73333L7.81675 7L11.0834 10.2667L10.2667 11.0833L7.00008 7.81667L3.73341 11.0833Z" fill="#235347"/>
        </svg>
      </button>
      <div class="good-popup__galary">
        <div class="good-popup__galary__body">
          <div class="slider">
            <!-- {{ activeItem }} -->
            <!-- <h1>{{ activeItem.name }}</h1> -->
            <div class="slider__slide" v-for="(el, index) in activeItem.galary" :key="index">
              <img :src="el" alt="" />
            </div>
          </div>
        </div>
        <div class="slider-indicators" v-if="activeItem.galary.length > 1">
          <div
            :class="['slider-indicators__indic', index == activeImg ? 'active-indic' : '']"
            v-for="(el, index) in activeItem.galary"
            :key="index"
            @click="scrollSlider(index)"
          >
            <img :src="el" alt="" />
          </div>
        </div>
      </div>
      <div class="good-popup__info">
        <div class="good-popup__info__wrapper">
            <h2 class="good-popup__info__subtitle">{{ activeItem.title }}</h2>
            <h1 class="good-popup__info__title">{{ activeItem.name }}</h1>
        </div>
        <div class="good-popup__info__wrapper">
            <div class="good-popup__info__wrapper__line">
                <h2 class="good-popup__info__wrapper__line__title">Материал</h2>
                <h3 class="good-popup__info__wrapper__line__param"><span v-for="(mat, index) in activeItem.material" :key="index">{{ index < activeItem.material.length -1 ? mat + ', ' : mat }}</span></h3>
            </div>
        </div>
        <div class="good-popup__info__wrapper">
            <h2 class="good-popup__info__another">Дополнительно</h2>
            <div class="good-popup__info__wrapper__line" v-for="(arr, index) in activeItem.another" :key="index">
                <h2 class="good-popup__info__wrapper__line__title">{{ arr[0] }}</h2>
                <h3 class="good-popup__info__wrapper__line__param">{{ arr[1] }}</h3>
            </div>
        </div>
        <div class="costNorder">
            <h2 class="costNorder__cost">{{ activeItem.cost }} ₽</h2>
            <ButtonComp />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ButtonComp from '../ButtonComp.vue';

export default {
    components: { ButtonComp },
  data() {
    return {
      isVisible: false,
      activeItem: {},
      activeImg: 0,
    };
  },
  methods: {
    openModal(item) {
      this.isVisible = true;
      this.activeItem = item;
      console.log(this.activeItem);
    },
    closeModal() {
      this.isVisible = false;
    },
    scrollSlider(i) {
        this.activeImg = i
        const slider = document.querySelector('.good-popup__galary__body')
        const slide_width = document.querySelector('.slider__slide').clientWidth
        slider.scrollTo(i * slide_width, 0)
    }
  },
};
</script>

<style scoped lang="scss">
h1,h2,h3,p{
    color: #000;
}
.good-popup {
  position: fixed;
  background: #000000a8;
  z-index: 20;
  left: 0;
  top: 0;
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
@media(max-width: 600px) {
    overflow-y: scroll;
}


  &__wrapper {
    position: relative;
    width: 1000px;
    height: max-content;
    background: #fff;
    border-radius: 16px;
    display: flex;
    flex-direction: row;
    gap: 25px;
    @media(max-width: 600px) {
        flex-direction: column;
        // height: unset;
        min-height: 100vh;
        height: max-content;
        overflow-y: scroll;
        border-radius: 0;
    }
    .close-btn{
      position: absolute;
      width: 20px;
      height: 20px;
      border-radius: 50%;
      border: none;
      outline: none;
      display: flex;
      align-items: center;
      justify-content: center;
      right: 20px;
      top: 20px;
    }
  }
  &__galary {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    padding: 20px 0 15px 20px;
    @media(max-width: 600px) {
        padding: 50px 15px 0 15px;
        width: 100%;
        // height: max-content;
    }

    &__body {
      width: 550px;
      // height: 367px;
      height: max-content;
      // padding-bottom: -15px;
      overflow-x: scroll;
      overflow-y: hidden;
      scroll-behavior: smooth;
      // padding-bottom: 20px !important;
      // padding: 0 !important;
      @media(max-width: 600px) {
        width: 90vw;
      }

      &::-webkit-scrollbar {
        width: 0;
      }
      .slider {
        height: 367px;
        display: flex;
        flex-direction: row !important;
        width: max-content;
        //   margin-bottom: 15px !important;
        @media(max-width: 600px) {
            height: unset;
        }

        &__slide {
            width: 550px !important;
            height: 367px !important;
            border-radius: 12px !important;
          // margin-bottom: 20px !important;
            @media(max-width: 600px) {
                width: 90vw !important;
                height: unset !important;
            }

          img {
            width: 100%;
            height: 100%;
            border-radius: 12px !important;
            @media(max-width: 600px) {
                width: 90vw;
                height: unset;
            }
          }
        }
      }
    }
    .slider-indicators {
      width: max-content;
      height: max-content;
      display: flex;
      flex-direction: row;
      align-items: center;
      gap: 10px;

      &__indic {
        width: 90px;
        height: 60px;
        border-radius: 6px;
        // transition: all 0.1s ease-out;
        &.active-indic{
            // border: 1px solid;
            width: 98px;
            height: 65px;
            @media(max-width: 600px) {
                width: 68px;
                height: 45px;
            }
        }
        @media(max-width: 600px) {
            width: 60px;
            height: 40px;
        }
        img {
          width: 100%;
          height: 100%;
          border-radius: 6px;
        }
      }
    }
  }
  &__info{
    padding: 20px 20px 15px 0;
    display: flex;
    flex-direction: column;
    gap: 30px;
    width: 100%;

    @media(max-width: 600px) {
        padding: 0 15px 15px 15px;
    }
    &__title{
        font-size: 40px;
        text-transform: uppercase;
        @media(max-width: 600px) {
            font-size: 24px;
        }
    }
    &__subtitle{
        font-size: 20px;
        text-transform: uppercase;
        color: #969696;
        font-weight: 500;
        @media(max-width: 600px) {
            font-size: 15px;
        }
    }
    &__another{
        margin-bottom: 10px;
        font-size: 20px;
        color: #969696;
        font-weight: 500;
        // text-transform: uppercase;
        @media(max-width: 600px) {
            font-size: 15px;
            margin-bottom: 5px;
        }
    }
    &__wrapper{
        padding-bottom: 10px;
        width: 100%;
        border-bottom: 1px solid #D9D9D9;

        &__line{
            display: flex;
            flex-direction: row;
            align-items: center;
            gap: 25px;

            &__title{
                font-size: 20px;
                text-transform: uppercase;
                width: max-content !important;
                @media(max-width: 600px) {
                    font-size: 14px;
                }
            }
            &__param{
                font-size: 16px;
                color: #969696;
                font-weight: 500;
                width: 100%;
                @media(max-width: 600px) {
                    font-size: 12px;
                }

                span{
                    font-size: 16px;
                    color: #969696;
                    font-weight: 500;
                    @media(max-width: 600px) {
                        font-size: 12px;
                    }
                }
            }
        }
    }
    .costNorder{
        display: flex;
        flex-direction: column;
        align-items: flex-end;
        gap: 25px;
        margin-top: 65px;
        @media(max-width: 600px) {
            gap: 20px;
            margin-top: 0;
        }

        .main-button{
            width: 250px !important;
        }
    }
  }
}
// img{
//     width: 100px;
//     height: 100px;
// }
</style>
