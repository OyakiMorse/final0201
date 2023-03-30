<template>
  <div>
    <div class="wrapper">
      <main class="profile">
        <div class="profile__info">
          <div class="profile__info-img">
            <img src="@/assets/img/photo.png" alt="profile-picture" />
          </div>

          <div class="profile__info-about">
            <h3 class="profile__info-username">Eva Jonson</h3>
            <p class="profile__info-position">Sales Manager</p>

            <p class="profile__info-text">
              I will find the best offers for you.<br />
              My services are absolutely free.
            </p>
          </div>
        </div>

        <div class="services">
          <h3 class="services__title">Services</h3>

          <div class="services__block">
            <div class="services__block-item">
              <div class="services__block-row">
                <p
                  class="services__block-row--bg"
                  :style="{ width: '90%', background: '#B1E19B' }"
                ></p>
                <h5 class="services__block-title">Manual tour booking</h5>
              </div>

              <span class="services__block-quantity">11</span>
            </div>

            <div class="services__block-item">
              <div class="services__block-row">
                <p
                  class="services__block-row--bg"
                  :style="{ width: '17%', background: '#ACE2F8' }"
                ></p>
                <h5 class="services__block-title">Package tours</h5>
              </div>

              <span class="services__block-quantity">3</span>
            </div>

            <div class="services__block-item">
              <div class="services__block-row">
                <p
                  class="services__block-row--bg"
                  :style="{ width: '12%', background: '#ACE2F8' }"
                ></p>
                <h5 class="services__block-title">Hotels</h5>
              </div>

              <span class="services__block-quantity">1</span>
            </div>
          </div>

          <div class="services__total">
            <p class="services__total-title">Total</p>
            <p class="services__total-quantity">15</p>
          </div>
        </div>

        <div class="reviews">
          <div class="reviews__header">
            <div class="reviews__header-info">
              <h2 class="reviews__latest">Latest reviews</h2>
              <button class="reviews__all">All reviews</button>
            </div>

            <div class="reviews__header-icons">
              <div class="reviews__icon">
                <img src="@/assets/img/like.svg" alt="comment" />
                131
              </div>

              <div class="reviews__icon">
                <img src="@/assets/img/comment.svg" alt="comment" />
                {{ reviews.length }}
              </div>
            </div>
          </div>

          <div class="reviews__wrapper">
            <div v-for="review in reviews" :key="review.id" class="review">
              <div class="review__header">
                <h6 class="review__username">{{ review.username }}</h6>
                <div class="review__date">
                  {{ review.date }}
                </div>
              </div>

              <div class="review__item">{{ review.msg }}</div>
            </div>
          </div>
        </div>
      </main>
    </div>

    <div class="wrapper-form">
      <form
        class="form"
        @keydown.ctrl.enter="submitReview"
        @submit.prevent="submitReview"
      >
        <textarea v-model="reviewData" class="form__textarea" name="textarea">
        </textarea>
        <button class="form__btn">Send a message</button>
      </form>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref, reactive } from "vue";
import moment from "moment";

interface ReviewItem {
  id: number;
  username: string;
  date: string;
  msg: string;
}

const reviewData = ref<string>(""),
  reviews = reactive<ReviewItem[]>([
    {
      id: Date.now(),
      username: "Samuel Jackson",
      date: "13 Apr 2022",
      msg: " Hey Eva! You're cool. Nice pic!",
    },
    {
      id: Date.now(),
      username: "Angela Deimon",
      date: "10 Apr 2022",
      msg: " Thanks for your services! We really liked the ocean view room. We hope to cooperate in the near future. We are sure you will do everything to makeour next holiday fantastic.",
    },
    {
      id: Date.now(),
      username: "Ronald Harris",
      date: "8 Apr 2022",
      msg: "Eva, hello! There is such a question: How can I contact you if I am abroad in roaming?",
    },
  ]);

function submitReview(): void {
  if (reviewData.value) {
    const currentDate: Date = new Date(),
      username: string = "Guest",
      date: string = moment(currentDate).format("d MMM YYYY"),
      review: ReviewItem = {
        id: Date.now(),
        username,
        date,
        msg: reviewData.value,
      };

    reviewData.value = "";
    reviews.unshift(review);
  }
}
</script>


