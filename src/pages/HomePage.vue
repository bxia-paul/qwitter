<template>
  <q-page class="relative-postion">
    <q-scroll-area class="absolute full-height full-width">
      <div class="q-py-lg q-px-md row items-end q-col-gutter-md">
        <div class="col">
          <q-input
            bottom-slots
            v-model="newTwitterContent"
            placeholder="What's happening?"
            counter
            maxlength="280"
            autogrow
            class="newTweet"
          >
            <template v-slot:before>
              <q-avatar size="xl">
                <img
                  src="https://pbs.twimg.com/media/EMb62bpW4AA43Er?format=jpg&name=small"
                />
              </q-avatar>
            </template>
          </q-input>
        </div>

        <div class="col col-shrink">
          <q-btn
            @click="addNewTweet"
            unelevated
            rounded
            color="primary"
            label="Tweet"
            no-caps
            :disable="!newTwitterContent"
            class="q-mb-lg"
          />
        </div>
      </div>

      <q-separator size="3px" color="grey-6" />

      <div class="q-pa-md q-gutter-md">
        <q-list separator>
          <transition-group
            appear
            enter-active-class="animated fadeIn slow"
            leave-active-class="animated fadeOut slower"
          >
            <q-item v-for="tweet in tweets" :key="tweet.date" class="q-py-md">
              <q-item-section avatar>
                <q-avatar top>
                  <img
                    src="https://pbs.twimg.com/media/EMb62bpW4AA43Er?format=jpg&name=small"
                  />
                </q-avatar>
              </q-item-section>

              <q-item-section>
                <q-item-label class="text-subtitle1">
                  <strong> Cels </strong>
                  <span class="text-grey-7"
                    >@cels <br class="lt-md" />
                    &bull; {{ tweet.date }}</span
                  >
                </q-item-label>

                <q-item-label class="tweetContent text-body1">
                  {{ tweet.content }}
                </q-item-label>

                <div class="row justify-between q-mt-sm">
                  <q-btn
                    flat
                    round
                    color="grey"
                    icon="far fa-comment"
                    size="sm"
                  />
                  <q-btn
                    flat
                    round
                    :color="tweet.retweeted ? 'green' : 'grey'"
                    icon="fas fa-retweet"
                    size="sm"
                    @click="reTweeted(tweet)"
                  />
                  <q-btn
                    flat
                    round
                    :color="tweet.liked ? 'pink' : 'grey'"
                    :icon="tweet.liked ? 'fas fa-heart' : 'favorite_border'"
                    size="sm"
                    @click="likeTweet(tweet)"
                  />
                  <q-btn
                    @click="deleteTweet(tweet)"
                    flat
                    round
                    color="grey"
                    icon="far fa-trash-alt"
                    size="sm"
                  />
                </div>
              </q-item-section>
            </q-item>

            <q-separator inset="item" />
          </transition-group>
        </q-list>
      </div>
    </q-scroll-area>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";
import { formatDistance } from "date-fns";

export default defineComponent({
  name: "HomePage",
  data() {
    return {
      newTwitterContent: "",
      tweets: [
        {
          content:
            " Can't wait for school to start back! Last semester !! Yay !!!",
          date: 161165323810,
          liked: false,
          retweeted: true,
        },
        {
          content: "Homework: If it goes too easy, you are doing it wrong.",
          date: 1611653238221,
          liked: true,
          retweeted: false,
        },
        {
          content:
            "That embarrassing moment when you realize, that person wasn't waving at you.",
          date: 1611653238443,
          liked: false,
          retweeted: false,
        },
        {
          content: "I need a 6 month holiday. Twice a year.",
          date: 1611653238667,
          liked: false,
          retweeted: false,
        },
        {
          content:
            "That awkward moment when somebody is doing dishes, and you slowly put another dish in the sink.",
          date: 1611653238879,
          liked: false,
          retweeted: false,
        },
      ],
    };
  },
  methods: {
    addNewTweet() {
      let newTweet = {
        content: this.newTwitterContent,
        date: Date.now(),
      };
      this.tweets.unshift(newTweet);
      this.newTwitterContent = "";
    },

    deleteTweet(tweet) {
      let dateToDelete = tweet.date;
      let index = this.tweets.findIndex((tweet) => tweet.date === dateToDelete);
      this.tweets.splice(index, 1);
    },

    likeTweet(tweet) {
      let dateOfLikedTweet = tweet.date;
      let index = this.tweets.findIndex(
        (tweet) => tweet.date === dateOfLikedTweet
      );

      if (this.tweets[index].liked == true) {
        this.tweets[index].liked = false;
      } else {
        this.tweets[index].liked = true;
      }
    },

    reTweeted(tweet) {
      let dateOfLikedTweet = tweet.date;
      let index = this.tweets.findIndex(
        (tweet) => tweet.date === dateOfLikedTweet
      );

      if (this.tweets[index].retweeted == true) {
        this.tweets[index].retweeted = false;
      } else {
        this.tweets[index].retweeted = true;
      }
    },
  },

  computed: {
    relativeDate(tweet) {
      let dateOfTweet = tweet.date;
      let index = this.tweets.findIndex(
        (tweet) => tweet.date === dateOfLikedTweet
      );
      return formatDistance(this.newTwitterContent[index].date, new Date());
    },
  },
});
</script>

<style lang="css">
.newTweet {
  font-size: 19px;
  line-height: 1.4 !important;
}

.tweetContent {
  white-space: pre-line;
}
</style>
