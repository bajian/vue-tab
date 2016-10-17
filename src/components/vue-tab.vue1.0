<template>
    <div class="tab-title-container">
        <li class="tab-title"
        v-for="title in tabtitles"
        :class="{'active': $index+1===currentPage}"
        track-by="$index"
        @click="setPage($index+1)">{{title}}</li>
    </div>
    <!-- decide if bind touchstart -->
    <div v-if="slideable"
    class="tabswiper"
    :class="{'invisible':invisible}"
    @touchstart="_onTouchStart">
    <div class="tabswiper-wrap"
    v-el:tabswiper-wrap
    :class="{'dragging': dragging}"
    :style="{'transform' : 'translate3d(' + translateX + 'px,0, 0)'}"
    @transitionend="_onTransitionEnd">
    <slot></slot>
</div>
</div> 
<div v-else class="tabswiper"
:class="{'invisible':invisible}">
<div class="tabswiper-wrap"
v-el:tabswiper-wrap
:class="{'dragging': dragging}"
:style="{'transform' : 'translate3d(' + translateX + 'px,0, 0)'}"
@transitionend="_onTransitionEnd">
<slot></slot>
</div>
</div> 
</template>

<script type="text/babel">

    const JUDGE_INITIAL=0
    const JUDGE_SLIDEING=1
    const JUDGE_SCROLLING=2

    export default {
        props: {
            tabtitles: {
                type: Array,
                default: []
            },
            currentPage: {
                type: Number,
                default: 1
            },
            slideable: {
                type: Boolean,
                default: true
            }
        },
        data() {
            return {
                lastPage: 1,
                translateX: 0,
                startTranslateX: 0,
                delta: 0,
                deltaY: 0,
                dragging: false,
                startPos: null,
                startPosY: null,
                transitioning: false,
                slideEls:[],
                invisible:true,
                judge:JUDGE_INITIAL,
            };
        },
        ready() {
            this._onTouchMove = this._onTouchMove.bind(this);
            this._onTouchEnd = this._onTouchEnd.bind(this);
            this.slideEls = this.$els.tabswiperWrap.children;
            this.dragging=true;
            this.setPage(this.currentPage);
            let _this=this;
            setTimeout(()=>{
                _this.dragging=_this.invisible=false;
            },100)
        },
        methods: {
            next() {
                var page = this.currentPage;
                if (page < this.slideEls.length) {
                    page++;
                    this.setPage(page);
                } else {
                    this._revert();
                }
            },
            prev() {
                var page = this.currentPage;
                if (page > 1) {
                    page--;
                    this.setPage(page);
                } else {
                    this._revert();
                }
            },
            setPage(page) {
                this.lastPage = this.currentPage;
                this.currentPage = page;

                this.translateX = -[].reduce.call(this.slideEls, function (total, el, i) {
                //previousValue,currentValue,currentIndex
                return i > page - 2 ? total : total + el['clientWidth'];
            }, 0);
                this._onTransitionStart();
            },
            _onTouchStart(e) {
                this.startPos = this._getTouchPos(e);
                this.startYPos = this._getTouchYPos(e);
                this.delta = 0;
                this.startTranslateX = this.translateX;
                this.startTime = new Date().getTime();
                this.dragging = true;

                document.addEventListener('touchmove', this._onTouchMove, false);
                document.addEventListener('touchend', this._onTouchEnd, false);
            },
            _onTouchMove(e) {
                this.delta = this._getTouchPos(e) - this.startPos;
                this.deltaY = Math.abs(this._getTouchYPos(e) - this.startYPos);


                switch (this.judge) {
                    case JUDGE_INITIAL:
                    // if (Math.abs(this.delta) > 20 && this.deltaY<25) {//judge to allow/prevent scroll
                    if (Math.abs(this.delta) / this.deltaY>1.5) {//judge to allow/prevent scroll
                        this.judge=JUDGE_SLIDEING
                        e.preventDefault();
                        e.stopPropagation()
                    }else{
                        this.judge=JUDGE_SCROLLING
                    }
                    break;
                    case JUDGE_SCROLLING:

                    break;
                    case JUDGE_SLIDEING:
                    this.translateX = this.startTranslateX + this.delta;
                    break;
                    
                    default:

                    break;
                }
                
            },
            _onTouchEnd(e) {
                if (this.judge==JUDGE_SLIDEING) {
                    this.dragging = false;
                    var isQuickAction = new Date().getTime() - this.startTime < 1000;
                    if (this.delta < -100 || (isQuickAction && this.delta < -15 && this.deltaY/this.delta>-6)) {
                        this.next();
                    } else if (this.delta > 100 || (isQuickAction && this.delta > 15 && this.deltaY/this.delta<6)) {
                        this.prev();
                    } else {
                        this._revert();
                    }
                }
                this.judge=JUDGE_INITIAL
                document.removeEventListener('touchmove', this._onTouchMove);
                document.removeEventListener('touchend', this._onTouchEnd);
            },
            _revert() {
                this.setPage(this.currentPage);
            },
            _getTouchPos(e) {
                var key = 'pageX' ;
                return e.changedTouches ? e.changedTouches[0][key] : e[key];
            },
            _getTouchYPos(e) {
                var key = 'pageY' ;
                return e.changedTouches ? e.changedTouches[0][key] : e[key];
            },
            _onTransitionStart() {
                this.transitioning = true;
                if (this._isPageChanged()) {
                    this.$emit('tab-change-start', this.currentPage);
                } else {
                    this.$emit('tab-revert-start', this.currentPage);
                }
            },
            _onTransitionEnd(e) {
                e.stopPropagation()
                if(e.target.className!='tabswiper-wrap') return;
                this.transitioning= false;
                if (this._isPageChanged()) {
                    this.$emit('tab-change-end', this.currentPage);
                } else {
                    this.$emit('tab-revert-end', this.currentPage);
                }
            },
            _isPageChanged() {
                return this.lastPage !== this.currentPage;
            }
        }
    };
</script>

<style type="text/css">

    .invisible{
        visibility:hidden;
    }
    .tabswiper {
      position: relative;
      overflow: hidden;
  }
  .tabswiper-wrap {
    display: flex;
    transition: all 0.4s ease;
    flex-direction: row;
}
.tabswiper-wrap.dragging{
    transition: none;
}
.tabswiper-wrap> div {
  overflow-x:hidden; 
  flex-shrink: 0;
  width: 100%;
  margin: 0px;
  padding: 0px;
}

::-webkit-scrollbar  
{  
    width: 0px;  
}  

.tab-title-container{
    position: relative;
    display: table;
    margin: 0 auto;
    list-style: none;
    border-bottom: 1px solid #dddddd;
    display: -webkit-flex;
    display: flex;
    flex-wrap: nowrap;
    align-items: center;
    justify-content: center;
}
.tab-title{
    height: 35px;
    line-height: 35px;
    position: relative;
    text-align: center;
    cursor: pointer;
    outline-style: none;
    flex: 1;
}
.tab-title.active,.tab-title:active {
    border-bottom: 2px solid #36acf4;
    color: #36acf4;
}
</style>
