<template>
  <div>
    <v-card v-if="skill.err" flat outlined>
      <v-card-text class="text-center pa-1">
        <span class="flavor-text subtle--text">// MISSING DATA //</span>
      </v-card-text>
    </v-card>
    <v-expansion-panels v-else focusable accordion style="border-radius: 0px">
      <v-expansion-panel
        :class="`text-center no-shadow ${noBorder ? '' : 'border-thin-primary '}`"
        :style="pilot ? 'border-color: var(--v-pilot-base)' : ''"
      >
        <v-expansion-panel-header :class="$vuetify.breakpoint.mdAndUp ? 'px-2' : 'py-1 px-2'">
          <v-row no-gutters>
            <v-col cols="12" md="3">
              <div class="centered text-left pl-2">
                <span class="stat-text">{{ skill.Trigger }}</span>
                <div v-if="bonus && $vuetify.breakpoint.mdAndUp">
                  <v-icon v-for="n in bonus" :key="skill.ID + n" color="secondary" small>
                    mdi-hexagon
                  </v-icon>
                  <span class="flavor-text subtle--text">(+{{ bonus }})</span>
                </div>
                <span v-else-if="bonus" class="font-weight-bold accent--text pl-2">
                  +{{ bonus }}
                </span>
              </div>
            </v-col>
            <v-col cols="12" md="9" align-self="center">
              <span class="body-text pl-2">{{ skill.Description }}</span>
            </v-col>
          </v-row>
        </v-expansion-panel-header>
        <v-expansion-panel-content v-if="skill.Detail">
          <v-row no-gutters>
            <v-col>
              <p class="text-left flavor-text mb-0">{{ skill.Detail }}</p>
            </v-col>
          </v-row>
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  name: 'skill-item',
  props: {
    bonus: {
      type: Number,
      required: false,
      default: 0,
    },
    skill: {
      type: Object,
      required: true,
    },
    noBorder: {
      type: Boolean,
      required: false,
    },
    pilot: {
      type: Boolean,
      required: false,
    },
  },
})
</script>
