<template>
  <div class="colorPicker">
     <div>
      <radial-color-picker
        aria-label="hue radial slider"
        v-model="hue"
        :hue=hue
        :saturation=saturation
        :luminosity=luminosity
        @input="selectBackgroundColor"
      />
    </div>
    <div>
      <h3>Select color saturation</h3>
      <input
        aria-label="saturation horizontal slider"
        aria-valuetext="percent saturation"
        type="range"
        v-model="saturation"
        @input="selectBackgroundColor"
      />
    </div>
    <div>
      <h3>Select color luminosity</h3>
      <input
        aria-label="luminosity horizontal slider"
        aria-valuetext="percent luminosity"
        type="range"
        v-model="luminosity"
        @input="selectBackgroundColor"
      />
    </div>
    <div>
      <h3>Select color transparency</h3>
      <input
        aria-label="transparency horizontal slider"
        aria-valuetext="percent transparency"
        type="range"
        min="5"
        v-model="alpha"
        @input="selectBackgroundColor"
      />
    </div>
  </div>
</template>

<script>
import ColorPicker from '@radial-color-picker/vue-color-picker';
export default {
  name: 'BgColorPicker',
  components: {
    'radial-color-picker': ColorPicker
  },
  // have the three parts of the color in the data of the app.
  data: function() {
    return {
      hue: 0,
      saturation: 100,
      luminosity: 50,
      alpha:100,
    }
  },
  // now we are deriving all three parts of an HSL color from the component's
  // data.
  methods: {
    selectBackgroundColor() {
      this.$emit(
        'backgroundColor-change',
        `hsl(${this.hue}, ${this.saturation}%, ${this.luminosity}%, calc(${this.alpha}/100))`,
      );
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import '~@radial-color-picker/vue-color-picker/dist/vue-color-picker.min.css';
</style>
