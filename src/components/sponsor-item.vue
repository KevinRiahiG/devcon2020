<template functional>
  <a class="sponsor-logo"
     target="_blank"
     :href="props.sponsor.url"
     :title="props.sponsor.partner + props.sponsor.slogan">
    <span class="sponsor-logo-cont">
      <img class="logo-white temp-bg"
           :src="$options.methods.imageResolve('white_' + props.sponsor.image)"
           :title="props.sponsor.partner + props.sponsor.slogan"
           :alt="props.sponsor.partner" />

      <img class="logo-col temp-bg"
           :src="$options.methods.imageResolve(props.sponsor.image)"
           :title="props.sponsor.partner + props.sponsor.slogan"
           :alt="props.sponsor.partner" />
    </span>
  </a>
</template>

<script>
export default {
  name: "SponsorItem",

  props: {
    sponsor: {
      type: Object,

      required: true,

      validator(value) {
        const keys = Object.keys(value);
        const MANDATORY_FIELDS = ["level", "partner", "url", "support"];

        for (let key in value) {
          const isMandatory = MANDATORY_FIELDS.includes(key);

          const isMissingValue = isMandatory && !value[key];
          if (isMissingValue) {
            console.error(`Missing mandatory value for "${key}"`);
            break;
          }
        }

        return true;
      }
    }
  },

  methods: {
    imageResolve(filename) {
      const isFilenameEmpty = !filename;
      if (isFilenameEmpty) {
        return "images/sponsors/placeholder.png";
      }

      return `images/sponsors/${filename}.png`;
    }
  }
};
</script>

<style lang="scss" scoped>
.temp-bg {
  background-color: #888;
}

.sponsor-logo {
  padding: 10px;
  &-cont {
    display: inline-block;
    position: relative;
  }
  .logo-col {
    opacity: 0;
    position: absolute;
    left: 0;
    top: 0;
  }
  &:hover {
    .logo-white {
      opacity: 0;
      transition: all 0.35s ease-out;
    }
    .logo-col {
      opacity: 1;
      transition: all 0.35s ease-out;
    }
  }
  &:last-child {
    padding: 5px;
  }
  display: block;
  img {
    display: block;
    width: 250px;
    height: auto;
    padding: 10px;
    // margin: 0 auto;
  }
}
</style>