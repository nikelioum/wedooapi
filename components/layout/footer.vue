<template>
  <footer class="footer">
    <div class="flex-wrap">
      <span v-if="version.name" class="mono">
        <a
          class="footer-link hide-on-small-screen"
          href="https://wedoo.gr"
          target="_blank"
          rel="noopener"
        >
          Powered by Wedoo Team
        </a>
        <!-- <span v-if="version.hash">
          -
          <a
            :href="'https://github.com/liyasthomas/postwoman/commit/' + version.hash"
            target="_blank"
            rel="noopener"
          >{{version.hash}}</a>
        </span> -->
        <!-- <span v-if="version.variant">({{version.variant}})</span> -->
      </span>
      <span>
        
        <v-popover>
          
          <template slot="popover">
            <div v-for="locale in availableLocales" :key="locale.code">
              <nuxt-link :to="switchLocalePath(locale.code)">
                <button class="icon" v-close-popover>
                  {{ locale.name }}
                </button>
              </nuxt-link>
            </div>
          </template>
        </v-popover>
      </span>
    </div>
  </footer>
</template>

<style scoped lang="scss">
.footer {
  flex-flow: column nowrap;
}

.footer-link {
  margin: 8px 16px;
  color: var(--fg-light-color);

  &:hover {
    color: var(--fg-color);
  }
}
</style>

<script>
import * as version from "../../.postwoman/version.json"

export default {
  data() {
    return {
      version: {},
    }
  },

  beforeMount() {
    // Set version data
    this.version = version.default
  },

  computed: {
    availableLocales() {
      return this.$i18n.locales.filter(({ code }) => code !== this.$i18n.locale)
    },
  },
}
</script>
