<template>
  <div>
    <ncform
      :form-schema="formSchema"
      form-name="your-form-name"
      v-model="formSchema.value"
      @submit="submit()"
    ></ncform>
    <hr />
    <el-button @click="submit()">Submit</el-button>
  </div>
</template>

<script>
import NcDxInput from "./components";

export default {
  created() {
    this.$ncformAddWidget({ name: "nc-dx-input", widget: NcDxInput });
  },
  data() {
    return {
      formSchema: {
        type: "object",
        properties: {
          demo: {
            type: "array",
            value: 'dx: ["a"]',
            // value: ["a", "b"],
            ui: {
              widget: "nc-dx-input",
              widgetConfig: {
                realWidget: {
                  widget: "select",
                  widgetConfig: {
                    multiple: true,
                    enumSource: [
                      {
                        value: 'daniel',
                        label: 'daniel'
                      },
                      {
                        value: 'sarah',
                        label: 'sarah'
                      }
                    ]
                  }
                }
              }
            }
          }
        },
        value: {}
      }
    };
  },
  methods: {
    submit() {
      this.$ncformValidate("your-form-name").then(data => {
        if (data.result) {
          console.log(this.$data.formSchema.value);
        }
      });
    }
  }
};
</script>
