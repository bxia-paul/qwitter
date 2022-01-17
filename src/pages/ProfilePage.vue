<template>
  <q-page>
    <div class="col-4">
      <q-img
        src="https://wallpaperaccess.com/full/1332989.jpg"
        :ratio="16 / 9"
        style="height: 250px"
      />
    </div>

    <q-item-section avatar class="q-pl-md">
      <q-avatar size="xl" top>
        <img
          src="https://pbs.twimg.com/media/EMb62bpW4AA43Er?format=jpg&name=small"
        />
      </q-avatar>

      <q-item-label class="text-subtitle1">
                  <strong> Cels </strong>
                  <span class="text-grey-7">@cels </span>     
      </q-item-label>

    </q-item-section>

    <div class="row ">
    <i class="fas fa-map-marker-alt q-ml-xl q-my-md"></i> 
    <q-item-label class="text-subtitle1 q-ml-xs q-mt-md" > Trinidad and Tobago  </q-item-label>
    <i class="fas fa-birthday-cake q-ml-xl q-my-md"></i> 
    <q-item-label class="text-subtitle1 q-ml-xs q-mt-md" >Born January 11th, 2000  </q-item-label>
    </div>

    <div class="row justify-between">
    <q-btn  class="q-ma-md text-capitalize" label="Tweets" />
    <q-btn  class="q-ma-md text-capitalize" label="Tweet & Replies" />
    <q-btn  class="q-ma-md text-capitalize" label="Media" />
    <q-btn  class="q-ma-md text-capitalize" label="Likes" />
    </div>
    

    <q-separator class="q-pt-xs"> </q-separator>

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

  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "ProfilePage",
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
  filters: {
    relativeDate(value) {
      return formatDistance(value, new Date());
    },
  },
});
</script>
