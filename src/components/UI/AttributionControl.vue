
<template></template>

<script>
  import baseMixin from '../../lib/mixin'
  import controlMixin from './controlMixin'

  export default {
    mixins: [baseMixin, controlMixin],
    props: {
      compact: {
        type: Boolean,
        default: true
      }
    },

    data() {
      return {
        control: undefined,
        map: undefined
      };
    },

    created() {
      this.control = new this.mapbox.AttributionControl({ compact: this.compact })
    },

    methods: {
      _deferredMount(payload) {
        this.map = payload.map
        this.map.addControl(this.control)
        this.$emit('mgl-attribution-control-added', this.control)
        payload.component.$off('mgl-load', this._deferredMount)
      }
    }
  };
</script>
