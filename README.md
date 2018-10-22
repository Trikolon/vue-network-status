# vue-network-status

This library provides two VueJS components:

**OnlineStatus**: Shows an icon with tooltip representing if the client is currently online or
offline.

**NetworkInfo**: Shows metrics about the internet connection using the
[browser Network Information API](https://developer.mozilla.org/en-US/docs/Web/API/Network_Information_API).
Currently browser support is limited. I found that
[Chrome for Android](https://play.google.com/store/apps/details?id=com.android.chrome) works best.


## Installation
```
npm i --save vue-network-status
```

## Usage

Import the desired components
``` javascript
import {NetworkInfo, OnlineStatus} from 'vue-network-status';
```

Register them in your component
``` javascript
export default {
  name: 'app',
  components: {
    NetworkInfo,
    OnlineStatus,
    HelloWorld,
  },
};
```

Add them in your html section
``` html
<NetworkInfo/>
<OnlineStatus/>
```

More example code can be found in [App.vue](/src/App.vue)

## Development & Demo

### Project setup
```
npm install
```

#### Compiles and hot-reloads for development
```
npm run serve
```

#### Compiles and minifies for production
```
npm run build
```

#### Run your tests
```
npm run test
```

#### Lints and fixes files
```
npm run lint
```
