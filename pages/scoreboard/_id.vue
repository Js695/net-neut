<style lang="scss">
@mixin scoreboard-card-btn($value-bg-color, $label-bg-color, $img-height) {
  background-color: $label-bg-color;

  .value-bg {
    background-color: $value-bg-color;

    &:after {
      border-left-color: $value-bg-color;
    }
  }

  img {
    height: $img-height;
  }

  &:hover {
    $percentage: 5%;
    background-color: darken($label-bg-color, $percentage);
    cursor: pointer;
    transition: background-color .2s;

    .value-bg {
      background-color: darken($value-bg-color, $percentage);
      transition: background-color .2s;

      &:after {
        transition: border-left-color .2s;
        border-left-color: darken($value-bg-color, $percentage);
      }
    }
  }
}

.scoreboard-id {
  .page-header {
    background-color: #14111b;

    h1 {
      font-size: 4rem;

      strong {
        font-weight: bold;
      }
    }

    .description {
      margin: 2rem 0 0;

      p {
        font-size: 1.8rem;
      }
    }

    .scoreboard-action-box {
      $color: #8c30ff;
      margin: 1rem auto -1rem;

      .btn {
        background-color: $color;

        &:hover {
          background-color: darken($color, 5%);
        }
      }

      .stats {
        color: $color;
      }
    }
  }

  &.against h1 strong {
    color: #ff4a4a;
  }

  &.supports h1 strong {
    color: #39c0a7;
  }

  section.boxes {
    position: relative;
    padding-top: 2rem;

    &:after {
      bottom: 100%;
      left: 50%;
      border: solid transparent;
      content: " ";
      height: 0;
      width: 0;
      position: absolute;
      pointer-events: none;
      border-color: rgba(136, 183, 213, 0);
      border-bottom-color: $alt-bg-color;
      border-width: 3rem;
      margin-left: -3rem;
    }

    .container {
      width: 45rem;
    }
  }

  .modal {
    h2 {
      font-size: 3.7rem;
    }
  }

  .petition-form {
    border: 0;
    padding: 0;

    .disclaimer {
      width: 96%;
      text-align: center;
    }
  }
}

.scoreboard-card {
  background-color: #322b45;
  border-radius: $border-radius;
  padding: 1.2rem;
  max-width: 45rem;
  margin: auto;
  display: flex;

  .scoreboard-photo {
    width: 17rem;
    height: auto;
    margin-bottom: 0;

    @include mobile {
      width: 15rem;
    }

    h5 {
      font-size: 1.8rem;
    }

    &.long-name h5 {
      font-size: 1.3rem;
    }
  }

  .buttons {
    width: 29rem;
    padding-left: 1rem;
    display: flex;
    flex-direction: column;

    button, .btn {
      flex: 1;
      min-height: 6.158rem;
      border-radius: $border-radius;
      font-size: 2.2rem;
      font-weight: 700;
      font-family: $body-font;
      text-transform: uppercase;
      border: none;
      background: transparent;
      margin-bottom: 0.6rem;
      padding: 0;
      color: #fff;
      display: flex;
      align-items: center;
      justify-content: center;
      position: relative;

      @include mobile {
        min-height: 3.459rem;
      }

      &:last-child {
        margin-bottom: 0;
      }

      &:hover {
        cursor: pointer;
      }

      .value-bg {
        border-radius: $border-radius 0 0 $border-radius;
        position: absolute;
        top: 0;
        left: 0;
        height: 100%;
        width: 36%;

        &:after {
          left: 100%;
          top: 50%;
          border: solid transparent;
          content: " ";
          height: 0;
          width: 0;
          position: absolute;
          pointer-events: none;
          border-color: rgba(136, 183, 213, 0);
          border-left-color: #88b7d5;
          border-width: 10px;
          margin-top: -10px;
        }
      }

      .value {
        width: 36%;
        position: relative;
      }

      .label {
        flex: 2;
        border-radius: 0 $border-radius $border-radius 0;
        position: relative;
        letter-spacing: 0.1rem;
        text-align: center;

        img {
          width: auto;
          margin-right: 0.5rem;
        }
      }

      &.call {
        @include scoreboard-card-btn(#188d49, #27d26f, 1.9rem);
      }

      &.write {
        @include scoreboard-card-btn(#6324b3, #8c30ff, 1.4rem);
      }

      &.tweet {
        @include scoreboard-card-btn(#1296b7, #1cc2ec, 1.6rem);
      }

      &.btn-facebook, &.btn-twitter, &.btn-volunteer {
        font-size: 1.8rem;

        &:before {
          content: none;
        }
      }

      &.btn-facebook {
        background-color: $facebook-blue;

        &:hover {
          background-color: darken($facebook-blue, 10%);
        }
      }

      &.btn-twitter {
        background-color: $twitter-blue;

        &:hover {
          background-color: darken($twitter-blue, 10%);
        }
      }

      &.btn-volunteer {
        background-color: #635686;

        &:hover {
          background-color: darken(#635686, 5%);
        }
      }
    }
  }
}

.scoreboard-action-box .share-buttons {
  .btn {
    font-size: 1.5rem;
    padding: 1.3rem;

    &:before {
      content: none;
    }

    &.btn-facebook {
      background-color: $facebook-blue;

      &:hover {
        background-color: darken($facebook-blue, 10%);
      }
    }

    &.btn-twitter {
      background-color: $twitter-blue;

      &:hover {
        background-color: darken($twitter-blue, 10%);
      }
    }
  }
}
</style>

<template>
  <div class="scoreboard-id" :class="status">
    <section class="page-header">
      <div class="container">
        <h1 v-html="titleHTML"></h1>

        <div class="scoreboard-card">
          <scoreboard-photo :rep="rep"></scoreboard-photo>

          <!-- FOR -->
          <div class="buttons" v-if="rep.supports_net_neutrality === true">
            <facebook-button :url="shareURL">{{ $lt('supports.facebook_button') }}</facebook-button>
            <twitter-button :url="twitterURL">{{ $lt('supports.twitter_button') }}</twitter-button>
            <a class="btn btn-volunteer" :href="volunteerURL">{{ $lt('supports.volunteer_button') }}</a>
          </div>

          <!-- AGAINST or NO STANCE -->
          <div class="buttons" v-else>
            <button class="call" @click="call()">
              <span class="value-bg" v-if="rep.call_count"></span>
              <span class="value" v-if="rep.call_count">{{ rep.call_count | formatNumber }}</span>
              <span class="label">
                <img src="~/assets/images/scoreboard-call-icon.svg" alt="">
                {{ $lt(`${status}.call_button`) }}
              </span>
            </button>
            <button class="write" @click="write()">
              <span class="value-bg" v-if="rep.letter_count"></span>
              <span class="value" v-if="rep.letter_count">{{ rep.letter_count | formatNumber }}</span>
              <span class="label">
                <img src="~/assets/images/scoreboard-write-icon.svg" alt="">
                {{ $lt(`${status}.write_button`) }}
              </span>
            </button>
            <button class="tweet" @click="tweet()" v-if="rep.twitter">
              <span class="value-bg" v-if="rep.tweet_count"></span>
              <span class="value" v-if="rep.tweet_count">{{ rep.tweet_count | formatNumber }}</span>
              <span class="label">
                <img src="~/assets/images/scoreboard-tweet-icon.svg" alt="">
                {{ $lt(`${status}.tweet_button`) }}
              </span>
            </button>
          </div>

        </div>

        <div class="description" v-html="descriptionHTML"></div>

        <!-- <scoreboard-action-box v-if="actionTeamURL"
          :title="$lt('action_team.title') "
          :description="$lt('action_team.description')"
          :cta_button="$lt('action_team.cta_button')"
          :cta_url="actionTeamURL"
        /> -->
      </div>
    </section>

    <section class="boxes">
      <div class="container">

        <!-- California scoreboard page -->
        <div v-if="isCalifornia">
          <scoreboard-action-box
            :title="$lt('california.boxes.facebook_group.title') "
            :description="$lt('california.boxes.facebook_group.description')"
            :cta_button="$lt('california.boxes.facebook_group.cta_button')"
            cta_url="https://www.facebook.com/groups/2079387388948963/"
          />

          <scoreboard-action-box
            :title="$lt('boxes.donate.title') "
            :description="$lt('boxes.donate.description')"
            :cta_button="$lt('boxes.donate.cta_button')"
            :cta_url="donateURL"
          />

          <scoreboard-action-box
            :title="$lt('california.boxes.scoreboard.title')"
            :description="$lt('california.boxes.scoreboard.description')"
            :cta_button="$lt('california.boxes.scoreboard.cta_button')"
            cta_url="/california/#scoreboard"
          />
        </div>

        <!-- Regular scoreboard page -->
        <div v-else>
          <scoreboard-action-box
            :title="$lt('boxes.events.title') "
            :description="$lt('boxes.events.description')"
            :cta_button="$lt('boxes.events.cta_button')"
            :cta_url="mapURL"
          />

          <scoreboard-action-box
            :title="$lt('boxes.business.title') "
            :description="businessBoxDescription"
            :cta_button="$lt('boxes.business.cta_button')"
            cta_url="https://www.businessesfornetneutrality.com"
           />

           <scoreboard-action-box
             :title="$lt('boxes.donate.title') "
             :description="$lt('boxes.donate.description')"
             :cta_button="$lt('boxes.donate.cta_button')"
             :cta_url="donateURL"
           />

           <scoreboard-action-box
             :title="$lt('boxes.scoreboard.title')"
             :description="$lt('boxes.scoreboard.description')"
             :cta_button="$lt('boxes.scoreboard.cta_button')"
             cta_url="/scoreboard/all"
           />
        </div>

        <scoreboard-action-box v-if="rep.supports_net_neutrality === false"
          :title="$lt('boxes.share.title') "
          :description="$lt('boxes.share.description')"
          class="share-box"
        >
          <div class="share-buttons flex-row">
            <facebook-button :url="shareURL" @clicked="$trackEvent('scoreboard_rep_facebook_share_button', 'click')">{{ $lt('boxes.share.facebook_button') }}</facebook-button>
            <twitter-button :url="twitterURL" @clicked="$trackEvent('scoreboard_rep_twitter_share_button', 'click')">{{ $lt('boxes.share.twitter_button') }}</twitter-button>
          </div>
        </scoreboard-action-box>
      </div>
    </section>

    <modal v-if="modalVisible">
      <call-form v-if="modal == 'call'" :in-modal="true" :page="callFormPage" :title="callFormTitle"></call-form>
      <petition-form v-else :in-modal="true" :title="$lt('petition_form_title')"></petition-form>
    </modal>
  </div>
</template>

<script>
import axios from 'axios'
import { createMetaTags, formatNumber, getDonateLink, openPopup } from '~/assets/js/helpers'
import ScoreboardPhoto from '~/components/ScoreboardPhoto'
import ScoreboardActionBox from '~/components/ScoreboardActionBox'
import ScoreboardForm from '~/components/ScoreboardForm'
import CallForm from '~/components/CallForm'
import PetitionForm from '~/components/PetitionForm'

async function fetchRep(bioguideId) {
  try {
    const { data } = await axios.get(`https://data.battleforthenet.com/scoreboard/${bioguideId}.json`)
    return data
  }
  catch (error) {
    return {}
  }
}

async function fetchBusinessCount(state) {
  try {
    const { data } = await axios.get(`https://data.battleforthenet.com/businesses/${state.toLowerCase()}.json`)
    return data.length
  }
  catch (error) {
    return null
  }
}

export default {
  components: {
    ScoreboardPhoto,
    ScoreboardActionBox,
    ScoreboardForm,
    CallForm,
    PetitionForm
  },

  head() {
    const vars = {
      name: this.repTitleAndName,
      amount: this.formattedContributions
    }

    const page = this.isCalifornia ? 'california' : 'scoreboard'

    return {
      title: this.$lt(`${this.status}.document_title`, vars),
      meta: createMetaTags({
        title: this.$t(`pages.${page}.social.title`),
        description: this.$t(`pages.${page}.social.description`),
        image: this.$t(`pages.${page}.social.image`),
        url: this.$t(`pages.${page}.social.url`)
      })
    }
  },

  data() {
    return {
      modalVisible: false,
      modal: null
    }
  },

  created() {
    if (this.isCalifornia) {
      this.$store.commit('setFacebookShareURL', this.shareURL)
      this.$store.commit('setTwitterShareURL', this.twitterURL)
    }
  },

  destroyed() {
    if (this.isCalifornia) {
      this.$store.commit('setFacebookShareURL', null)
      this.$store.commit('setTwitterShareURL', null)
    }
  },

  async asyncData(context) {
    const rep = await fetchRep(context.route.params.id)
    const bizCount = await fetchBusinessCount(rep.state)

    return {
      rep: rep,
      businessCount: bizCount
    }
  },

  computed: {
    status() {
      const stance = this.rep.supports_net_neutrality
      if (stance === true) {
        return 'supports'
      } else if (stance === false) {
        return 'against'
      } else {
        return 'neutral'
      }
    },

    repTitle() {
      switch (this.rep.organization) {
        case 'Senate':
          return 'senator'
        case 'Assembly':
          return 'assembly member'
        case 'House':
        default:
          return 'representative'
      }
    },

    repTitleAndName() {
      let title = ''

      switch (this.rep.organization) {
        case 'Senate':
          title = 'Senator'
          break
        case 'House':
          title = 'Rep.'
          break
        case 'Assembly':
          title = 'Asm.'
          break
      }

      return `${title} ${this.rep.first_name} ${this.rep.last_name}`
    },

    titleHTML() {
      let key = `${this.status}.title_html`

      if (this.isCalifornia) {
        key = `california.${key}`
      }

      return this.$lt(key, {
        title: this.repTitle
      })
    },

    descriptionHTML() {
      if (this.isCalifornia) {
        return this.$lt(`california.${this.status}.description_html`, {
          name: this.repTitleAndName
        })
      }
      else if (this.rep.supports_net_neutrality === false && !this.rep.cable_contributions) {
        return this.$lt(`${this.status}.no_amount_description_html`, {
          name: this.repTitleAndName
        })
      }
      else {
        return this.$lt(`${this.status}.description_html`, {
          name: this.repTitleAndName,
          amount: this.formattedContributions
        })
      }
    },

    formattedContributions() {
      if (this.rep.cable_contributions) {
        return '$' + formatNumber(this.rep.cable_contributions)
      }
      return null
    },

    shareURL() {
      return `https://www.battleforthenet.com/scoreboard/${this.rep.bioguide_id}/`
    },

    tweetText() {
      let key = `${this.status}.tweet_text`

      if (this.isCalifornia) {
        key = `california.${key}`
      }

      return this.$lt(key, {
        twitter: this.rep.twitter,
        url: this.shareURL
      })
    },

    twitterURL() {
      return `https://twitter.com/intent/tweet?text=${encodeURIComponent(this.tweetText)}`
    },

    // TODO: fill this in
    actionTeamURL() {
      return ''
    },

    volunteerURL() {
      if (this.isCalifornia) {
        return 'https://www.facebook.com/groups/2079387388948963/'
      }
      else {
        return '/map/'
      }
    },

    businessBoxDescription() {
      const bizCount = this.businessCount ? formatNumber(this.businessCount) : 'Many'
      return this.$lt('boxes.business.description', {
        count: bizCount
      })
    },

    donateURL() {
      return getDonateLink(this.$store.state.org)
    },

    mapURL() {
      let url = 'https://www.battleforthenet.com/map/'

      if (this.$store.state.zipCode) {
        url += `?zip=${this.$store.state.zipCode}`
      }

      return url
    },

    isCalifornia() {
      return !!this.$route.params.id.match(/^CA-/)
    },

    callFormPage() {
      if (this.isCalifornia) {
        return 'california'
      }
      else {
        return 'scoreboard'
      }
    },

    callFormTitle() {
      if (this.isCalifornia) {
        return this.$lt('california.call_form_title')
      }
      else {
        return this.$lt('call_form_title')
      }
    }
  },

  methods: {
    $lt(key, vars={}) {
      return this.$t(`pages.scoreboard.id.${key}`, vars)
    },

    call() {
      this.$trackEvent('scoreboard_rep_call_button', 'click')
      this.modal = 'call'
      this.modalVisible = true
    },

    write() {
      this.$trackEvent('scoreboard_rep_write_button', 'click')

      if (this.isCalifornia) {
        const district = this.rep.bioguide_id.replace(/^CA-/, '')
        openPopup(`https://lcmspubcontact.lc.ca.gov/PublicLCMS/ContactPopup.php?district=${district}&inframe=Y`, 'write', 640, 600)
      }
      else {
        this.modal = 'write'
        this.modalVisible = true
      }
    },

    tweet() {
      this.$trackEvent('scoreboard_rep_tweet_button', 'click')
      openPopup(this.twitterURL, 'share')
    }
  }
}
</script>
