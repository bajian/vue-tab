# vue-tab
###a tab that can be silded to change pages and allow different height、verticle scroll
> A Vue.js project

##demo

[online-demo](https://cdn.rawgit.com/bajian/vue-tab/master/dist/demo2.html)

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# run unit tests
npm run unit

# run e2e tests
npm run e2e

# run all tests
npm test
```

```html
	<!-- vue data to set tab title: 'tabtitles':['bajian','github'] -->
    <tab :tabtitles="tabtitles" 
    :current-page="3">
    <!-- div contain as each page -->
      <div class="tab-content-container">
        <div>hahaha1</div>
        <img src="http://i2.....">
        <div>hahaha1</div>
        <div>hahaha1</div>
        <img src="http://i2....">
      </div>
      <div class="tab-content-container">
        bajian2
      </div>
    </tab>

```

## Api
### Properties
| Name                 | Type      | Default      | Description                                                        |
|----------------------|-----------|--------------|--------------------------------------------------------------------|
| tabtitles            | `Array`  | `[]` | vue data to set tab title.         |
| current-page      | `Number` | `1`      | set the current active page start from 1. |
| slideable      | `Boolean` | `true`      | set false to disable silde to change a page. |
| ==================== | ========= | ============ | =================== |

>the length of tabtitles should match to the page number

### Events
| Name                            | Parameters | Description                                                                                                                                                  |
|--------------------|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| slide-change-start | `pageNumber`     | Fire in the beginning of animation to other slide (next or previous).                                                                                        |
| slide-change-end   | `pageNumber`     | Will be fired after animation to other slide (next or previous).                                                                                             |
| slide-revert-start | `pageNumber`     | Fire in the beginning of animation to revert slide (no change).                                                                                              |
| slide-revert-end   | `pageNumber`     | Will be fired after animation to revert slide (no change).                                                                                                   |
| slider-move        | `offset`         | Callback function, will be executed when user touch and move finger over page and move it. Receives swiper instance and 'touchmove' event as an arguments. |
| ================== | ================ | ============================ |

For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
