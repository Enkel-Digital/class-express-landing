<template>
  <section class="section hero is-fullheight has-text-left">
    <!-- Empty span tag here and below to force the actual content to be in the middle of the hero section vertically -->
    <span />

    <div class="columns">
      <!-- Embed a youtube video here to show how to install the App on IOS or android or how to use it -->
      <!-- Only shown on desktop, and hidden for mobile/tablet sizes. -->
      <!-- On mobile/tablets, clicking it opens the youtube link in new tab or youtube app -->
      <div id="youtubeVideo" class="column">
        <p class="title">{{ videoName }}</p>

        <iframe
          :src="videoIFrameSrc + preferencesString"
          frameborder="0"
          allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
          allowfullscreen
          width="100%"
          height="100%"
        />
      </div>

      <div class="column">
        <div class="columns is-multiline">
          <div class="column is-12 mb-6">
            <div class="container mx-4">
              <h1 class="title">Installing the App</h1>
              <h2 class="subtitle">
                Class Express is a Web App <sub>(PWA)</sub>, meaning SMALLER and
                Faster installs, while always being up to date.
              </h2>
            </div>

            <br />

            <!-- Here are big tiles as buttons, that I can click to show how to download / use on IOS and or Android -->
            <div class="columns is-multiline">
              <div
                class="column card features-card is-5"
                @click="switchVideo(videoConfigs.install_ios)"
              >
                <p class="title">IOS</p>
                <p>
                  Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin
                  ornare magna eros, eu pellentesque tortor vestibulum ut.
                  Maecenas non massa sem. Etiam finibus odio quis feugiat
                  facilisis.
                </p>
              </div>
              <div
                class="column card features-card is-5"
                @click="switchVideo(videoConfigs.install_android)"
              >
                <p class="title">Android</p>
                <p>
                  Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin
                  ornare magna eros, eu pellentesque tortor vestibulum ut.
                  Maecenas non massa sem. Etiam finibus odio quis feugiat
                  facilisis.
                </p>
              </div>
            </div>
          </div>

          <div class="column is-12">
            <div class="container mx-4">
              <h1 class="title">How to use</h1>
              <h2 class="subtitle">Learn the basics of the App</h2>
            </div>

            <br />

            <!-- Here are big tiles as buttons, that I can click to show how to download / use on IOS and or Android -->
            <div class="columns is-multiline">
              <div
                class="column card features-card is-5"
                @click="switchVideo(videoConfigs.gettingStarted)"
              >
                <p class="title">Getting Started</p>
                <p>
                  Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin
                  ornare magna eros, eu pellentesque tortor vestibulum ut.
                  Maecenas non massa sem. Etiam finibus odio quis feugiat
                  facilisis.
                </p>
              </div>
              <div
                class="column card features-card is-5"
                @click="switchVideo(videoConfigs.findClass)"
              >
                <p class="title">Find a new Class</p>
                <p>
                  Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin
                  ornare magna eros, eu pellentesque tortor vestibulum ut.
                  Maecenas non massa sem. Etiam finibus odio quis feugiat
                  facilisis.
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Empty span tag here and on top to force the actual content to be in the middle of the hero section vertically -->
    <span />
  </section>
</template>

<script>
export default {
  name: "Download",

  created() {
    // @todo Replace this makeshift solution with smth that Detect what device, and show the ios or android loading one
    if (!this.ifMobileOrTablet())
      this.switchVideo(this.videoConfigs.install_ios);
  },

  data() {
    //   @todo Explore the enableJsonAPI URL query parameter

    const preferences = {
      cc_lang_pref: "en",
      cc_load_policy: "1",

      // autoplay: "1", // To enable this, need to either set playlist value or set mute to true

      // loop: "1",
      // playlist: "86D7AGm5sHk", // To enable autoplay, the playlist must be set to the video ID
    };

    const preferencesString =
      "?" +
      Object.keys(preferences)
        .map((key) => `${key}=${preferences[key]}&`)
        .join("");

    console.log(preferencesString);

    return {
      videoName: "",
      videoIFrameSrc: "",
      preferencesString,

      videoConfigs: {
        install_ios: {
          videoIFrameSrc: "https://www.youtube-nocookie.com/embed/86D7AGm5sHk",
          videoName: "Install for IOS", // ios 13 and above for the new UI
        },
        install_android: {
          videoIFrameSrc: "https://www.youtube-nocookie.com/embed/egHjkeiqjrA",
          videoName: "Install for Android",
        },
        gettingStarted: {
          videoIFrameSrc: "https://www.youtube-nocookie.com/embed/w0P0FQ770dE",
          videoName: "Getting Started",
        },
        findClass: {
          videoIFrameSrc: "https://www.youtube-nocookie.com/embed/hs1HoLs4SD0",
          videoName: "Find a New Class",
        },
      },
    };
  },

  methods: {
    ifMobileOrTablet() {
      return (
        Math.max(
          document.documentElement.clientWidth || 0,
          window.innerWidth || 0
        ) < 1024
      );
    },

    switchVideo(videoConfig) {
      // Just like a media query, where this is true if using tablet or mobile device
      if (this.ifMobileOrTablet())
        return window.open(
          `https://youtube.com/watch?v=${videoConfig.videoIFrameSrc.slice(39)}`,
          "_blank"
        );

      this.videoIFrameSrc = videoConfig.videoIFrameSrc;
      this.videoName = videoConfig.videoName;
    },
  },
};
</script>

<style scoped>
.features-card {
  border-radius: 1em;
  border: 1px solid rgb(220, 220, 220);
  margin: 1em;

  cursor: pointer;
}

/* Change background depending on screen size */
#youtubeVideo {
  display: run-in;
}
/* Might change table to show it */
@media (max-width: 1024px) {
  #youtubeVideo {
    display: none;
  }
}
@media (max-width: 768px) {
  #youtubeVideo {
    display: none;
  }
}
</style>
