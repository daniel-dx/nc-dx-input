<template>
  <div class="nc-dx-input">
    <!-- disabled / readonly / placeholder / hidden : use the computed version, not the config version. -->
    <!-- modelVal: for binding value. -->
    <el-input style="flex: 1" v-show="isDxMode" v-model="dxVal" @change="handleDXChange">
      <template slot="prepend">dx:</template>
    </el-input>

    <ncform v-if="!onlyDXMode" style="flex: 1; margin: -15px -15px -10px"
      v-show="!isDxMode"
      :form-schema="formSchema"
      :form-name="formName"
      v-model="formVal"
      :is-dirty.sync="isFormDirty"
    ></ncform>

    <el-switch v-if="!onlyDXMode" style="margin: 8px" v-model="isDxMode" active-text="DX" @change="handleDXModeChange"></el-switch>
  </div>
</template>

<style lang="scss" scoped>
.nc-dx-input {
  display: flex;
}
</style>

<script>
import ncformCommon from "@ncform/ncform-common";

export default {
  mixins: [ncformCommon.mixins.vue.controlMixin],

  i18nData: {
    // i18n
    en: {
    },
    zh_cn: {
    }
  },

  created() {
    this.$data.onlyDXMode = !this.mergeConfig.realWidget.widget;
    if ((typeof this.modelVal === 'string' && this.modelVal.indexOf('dx:') === 0) || this.$data.onlyDXMode) { // is dx expression string value
      this.$data.isDxMode = true;
      this.$data.dxVal = String(this.modelVal).replace('dx:', '');
    } else {
      this.$data.isDxMode = false;
      this.formVal = {
        value: this.modelVal
      }
    }
  },

  data() {
    return {
      formName: "dx-input_" + ncformCommon.ncformUtils.genRandomId(),
      isDxMode: true,
      onlyDXMode: false,

      isFormDirty: false,
      formVal: {},
      dxVal: '',

      defaultConfig: {
        // your config's default value ( Note: use mergeConfig to get config value )
        realWidget: {
          widget: "",
          widgetConfig: {}
        }
      }
    };
  },

  computed: {
    formSchema() {
      return {
        type: "object",
        properties: {
          value: {
            type: "string",
            ui: {
              noLabelSpace: true,
              widget: this.mergeConfig.realWidget.widget,
              widgetConfig:  this.mergeConfig.realWidget.widgetConfig
            }
          }
        }
      };
    }
  },

  watch: {
    isFormDirty(newVal) {
      if (newVal) {
        this.$data.isFormDirty = false;
        !this.$data.isDxMode && (this.modelVal = this.$data.formVal.value);
      }
    },
  },

  methods: {

    handleDXModeChange() {
      // Set the correct value when switching modes
      if (this.$data.isDxMode) {
        this.modelVal = `dx: ${this.$data.dxVal.trim()}`
      } else {
        this.modelVal = this.$data.formVal.value
      }
    },

    handleDXChange() {
      this.modelVal = `dx: ${this.$data.dxVal.trim()}`
    },

    // you can handle the modelVal before $emit it ( before this.$emit('input') )
    _processModelVal(modelVal) {
      return modelVal;
    }

    // you can use this.$http to make some http requests ( this.$http is the same as axios )
  }
};
</script>
