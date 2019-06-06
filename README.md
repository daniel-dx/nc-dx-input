# nc-dx-input

nc-dx-input widget for [ncform](https://github.com/ncform/ncform)

![](https://raw.githubusercontent.com/daniel-dx/nc-dx-input/master/preview.gif)

## Install and basic usage

```
npm i -s nc-dx-input
```

**Add the widget**

```
import ncDxInput from 'nc-dx-input';

Vue.use(vueNcform, { extComponents: {ncDxInput} });

// or vm.$ncformAddWidget({name: 'ncDxInput', widget: ncDxInput});

```

**Use the widget**

```
{
  "type": "object",
  "properties": {
    "name": {
      "type": "array",
      "widget": "nc-dx-input",
      "widgetConfig": {
        "realWidget": {
          "widget": "select",
          "widgetConfig": {
            "multiple": true,
            "enumSource": [
              {
                "value": "daniel",
                "label": "daniel"
              },
              {
                "value": "sarah",
                "label": "sarah"
              }
            ]
          }
        }
      }
    }
  }
}
```

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

You only need to care about `src/components/index.vue`

### Compiles and minifies for production
```
npm run build
```

### Run your tests
```
npm run test
```

### Lints and fixes files
```
npm run lint
```

### Run your end-to-end tests
```
npm run test:e2e
```

### Run your unit tests
```
npm run test:unit
```
