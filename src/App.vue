<template>
  <div id="app">
    <div class="slideshow">
      <slide leave="fadeOut">
        <h1>Bridging the gap</h1>
        <p class="subtitle">with design systems</p>
        <div class="footer">
          Björn Ganslandt
          <br />
          <a href="https://twitter.com/Ansimorph">@ansimorph</a>
        </div>
      </slide>

      <slide leave="fadeOut">
        <h1>Bridging the gap</h1>
        <p class="subtitle">Between design & development</p>
      </slide>
      <slide leave="fadeOut" :steps="2">
        <h1>Design systems are no silver bullet</h1>
        <p class="subtitle" v-if="step >= 2">Communication is</p>
      </slide>
      <slide leave="fadeOut">
        <h1>Involve everyone from the start to find a shared language</h1>
      </slide>
      <slide leave="fadeOut">
        <h1>
          <span class="blue">Stay helpful</span> by keeping everyone in sync afterwards
        </h1>
      </slide>
      <slide leave="fadeOut" :steps="3">
        <ol class="numbered-list">
          <li v-if="step >= 1">Version/ Host design assets with Design System</li>
          <li v-if="step >= 2">Generate design assets from Design System</li>
          <li v-if="step >= 3">Design with code</li>
        </ol>
      </slide>

      <slide leave="fadeOut">
        <h1>Bridging the gap</h1>
        <p class="subtitle">Between Teams</p>
      </slide>
      <slide leave="fadeOut" :steps="3">
        <h1 v-if="step === 1">Starting small is easy</h1>
        <h1 v-if="step >= 2">The real work starts at team 2</h1>
        <team-graph class="illustration" :step="step"></team-graph>
      </slide>
      <slide leave="fadeOut" :steps="3">
        <ol class="numbered-list">
          <li v-if="step >= 1">Scaling requirements engineering across teams</li>
          <li v-if="step >= 2">Defining responsibilities</li>
          <li v-if="step >= 3">Sharing code</li>
        </ol>
      </slide>

      <slide leave="fadeOut">
        <h1>Bridging the gap</h1>
        <p class="subtitle">Between Technologies</p>
      </slide>
      <slide leave="fadeOut">
        <h1>Bridging the gap</h1>
        <div class="subtitle">
          <ul class="framework-icons">
            <li>
              <img class="framework-icons__item" src="./assets/images/react.svg" />
            </li>
            <li>
              <img class="framework-icons__item" src="./assets/images/angular.svg" />
            </li>
            <li>
              <img class="framework-icons__item" src="./assets/images/jquery.svg" />
            </li>
          </ul>
        </div>
      </slide>
      <slide class="pure-html" leave="fadeOut" :steps="3">
        <h1>HTML is there for you</h1>
        <div class="illustration">
          <hr />
          <br />
          <p v-if="step === 2">HTML / CSS are the smallest common denominators</p>
          <p v-if="step === 3">Webcomponents if you are brave</p>
        </div>
      </slide>
      <slide leave="fadeOut">
        <h1>Bridging the gap</h1>
        <div class="subtitle">
          <ul class="framework-icons">
            <li>
              <span class="framework-icons__item">&lt;html/&gt;</span>
            </li>
            <li>
              <img class="framework-icons__item" src="./assets/images/apple.svg" />
            </li>
            <li>
              <img class="framework-icons__item" src="./assets/images/android.svg" />
            </li>
          </ul>
        </div>
      </slide>
      <slide leave="fadeOut" :steps="2">
        <h1>Design tokens are there for you</h1>
        <div class="subtitle">
          <p v-if="step === 2">Also, react native or hybrid apps if you are brave</p>
        </div>
      </slide>

      <slide leave="fadeOut">
        <h1>Bridging the gap</h1>
        <p class="subtitle">Between Users</p>
      </slide>
      <slide leave="fadeOut" :steps="2">
        <h1>Design systems demand more quality of its components</h1>
        <p class="subtitle" v-if="step >= 2">So make them accessible</p>
      </slide>
      <slide class="pure-html" leave="fadeOut" :steps="4">
        <h1>HTML is there for you</h1>
        <div class="illustration">
          <hr />
          <br />
          <template v-if="step >= 2">
            <button>It's the biggest design system out there</button>
            <br />
            <br />
          </template>
          <template v-if="step >= 3">
            <a href="#">So use a link when linking and a button for actions</a>
            <br />
            <br />
          </template>
          <template v-if="step >= 4">
            There's even a slider:
            <img src="./assets/images/cool.gif" />
            <br />
            <br />
            <input type="range" name="points" min="0" max="10" />
          </template>
        </div>
      </slide>

      <slide leave="fadeOut">
        <div class="credits">
          <p class="h2size margin-small">Follow Me On Twitter:</p>
          <p class="margin-large">
            <a class="h3size" href="https://twitter.com/Ansimorph">@ansimorph</a>
          </p>
          <p class="h2size margin-small">Get the slides:</p>
          <a
            class="h3size"
            href="https://github.com/Ansimorph/bridging/"
          >github.com/Ansimorph/bridging/</a>
        </div>
      </slide>
    </div>
  </div>
</template>

<script>
import { Slideshow } from "eagle.js";
import Hammer from "hammerjs";
import TeamGraph from "./components/TeamGraph";

export default {
  name: "app",
  components: { "team-graph": TeamGraph },
  mixins: [Slideshow],
  props: {
    mouseNavigation: { default: false }
  },
  data: function() {
    return {
      baseUrl: process.env.BASE_URL
    };
  },
  mounted: function() {
    window.addEventListener("keydown", this.extraKeyboardNav);

    const hammer = new Hammer(document.querySelector(".slideshow"));
    hammer.on("swiperight", () => {
      this.previousStep();
    });
    hammer.on("swipeleft", () => {
      this.nextStep();
    });
  },
  methods: {
    // Also allow for navigation with up/down/Enter so that my presenter works
    extraKeyboardNav: function(event) {
      if (
        event.key === "ArrowUp" ||
        event.key === "Enter" ||
        event.key === " "
      ) {
        this.nextStep();
        event.preventDefault();
      } else if (event.key === "ArrowDown") {
        this.previousStep();
        event.preventDefault();
      }
    }
  }
};
</script>

<style lang="scss">
@import "./assets/fonts/plex/css/ibm-plex.css";
@import "./variables.scss";
@import "./base.scss";

h1,
h2,
h3,
.h1size,
.h2size,
.h3size {
  font-weight: 400;
  line-height: 1.1;
}

h1,
.h1size {
  grid-area: headline;
  font-size: $h1size;
  margin: 0;
  max-width: 10em;
  text-transform: capitalize;
}

h2,
.h2size {
  font-size: $h2size;
}

h3,
.h3size {
  font-size: $h3size;
}

a {
  color: $blue;
  text-decoration: none;

  &:hover {
    text-decoration: underline;
  }

  &:active {
    color: lighten($blue, 10%);
  }
}

p {
  margin-top: 0;
  margin-bottom: $space;
}

.margin-small {
  margin-bottom: $space * 2;
}

.margin-medium {
  margin-bottom: $space * 4;
}

.margin-large {
  margin-bottom: $space * 12;
}

.vertical-center {
  display: flex;
  flex-direction: column;
  justify-content: center;
  height: 100%;
}

.horizontal-center {
  display: flex;
  flex: 1;
  justify-content: center;
}

.fade-enter-active,
.fade-leave-active {
  transition: all 0.3s;
  transform: translateY(0);
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
  transform: translateY(20%);
}

.eg-slide-content {
  display: grid;
  grid-template:
    "headline" min-content
    "subtitle" min-content
    "illustration" 1fr
    "footer" min-content;
}

.illustration {
  margin-top: ($space * 2);
  grid-area: illustration;
  font-size: $h3size;
}

.subtitle {
  margin: ($space * 2) 0 0 0;
  font-size: $h1size;
  line-height: 1.1;
  grid-area: subtitle;
  max-width: 10em;
  color: $blue;
  text-transform: capitalize;
}

.footer {
  grid-area: footer;
}

.blue {
  color: $blue;
}

.numbered-list {
  margin: 0;
  max-width: 15em;
  padding: 0;
  list-style: none;
  font-size: $h2size;

  > li {
    display: flex;
    counter-increment: list-counter;
    margin-bottom: $space * 4;

    &::before {
      display: block;
      margin-right: $space * 2;
      color: $blue;
      content: counter(list-counter) ". ";
    }
  }
}

// Very slide-specifc stuff
.credits {
  margin-top: $space * 20;
}

.pure-html {
  background-color: #b2b2b2;
  color: unset;
  font-family: unset;

  .subtitle {
    color: unset;
  }

  a {
    color: blue;
    text-decoration: underline;
  }

  button {
    font-size: $h3size;
  }
}

.framework-icons {
  margin: 0;
  padding: 0;
  list-style: none;
  display: flex;
  align-items: center;
}

.framework-icons__item {
  height: $h4size;
  margin-top: $space * 2;
  margin-right: $h4size;
  text-transform: lowercase;
  line-height: 1;
  font-size: 0.9em;
  vertical-align: sub;
}
</style>
