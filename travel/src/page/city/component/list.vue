<template>
  <div class="list" ref="wrapper">
      <div>
        <div class="area">
            <div class="title border-topbottom">当前城市</div>
            <div class="button-list">
                    <div class="button-wrapper">
                        <div class="button">{{this.$store.state.city}}</div>
                    </div>
            </div>
        </div>
        <div class="area">
            <div class="title border-topbottom">热门城市</div>
            <div class="button-list">
                <div
                    class="button-wrapper"
                    v-for="item of hot"
                    :key="item.id"
                    @click="handCityClick(item.name)"
                >
                    <div class="button">{{item.name}}</div>
                </div>
            </div>
        </div>
        <div class="area" v-for="(item,key) of city" :key="key" :ref="key" >
            <div class="title border-topbottom">{{key}}</div>
            <div class="item-list" v-for="innerItem of item" :key="innerItem.id" @click="handCityClick(innerItem.name)">
                <div class="item  border-bottom">{{innerItem.name}}</div>
            </div>
        </div>
      </div>
  </div>
</template>
<script>
import BScroll from 'better-scroll'
export default {
  name:"CityList",
  props:{
      hot:Array,
      city:Object,
      letter:String
  },
  watch:{
      letter(){
          if(this.letter){
              const element = this.$refs[this.letter][0]
              this.scroll.scrollToElement(element)
          }
      }
  },
  methods: {
      handCityClick(city){
          this.$store.dispatch('changeCity',city)
          this.$router.push('/')
      }
  },
   mounted(){
      this.scroll = new BScroll(this.$refs.wrapper)
  },
}
</script>
<style lang="less" scoped>
.list{
    position: absolute;
    top: 1.58rem;
    left: 0;
    right: 0;
    bottom: 0;
    overflow: hidden;
    .area{
        .title{
            height: .54rem;
            line-height:.44rem;
            background: #f8f8f8;
            color: #666;
            padding: 0 .2rem;
            font-size: .26rem;
        }
        .button-list{
            padding: .1rem .6rem .1rem .1rem;
            overflow: hidden;
            .button-wrapper{
                    width: 33.33%;
                    float: left;
                .button{
                    margin: .1rem;
                    border:.02rem solid #ccc;
                    text-align: center;
                    padding:.1rem 0;
                    border-radius: .06rem;
                }
            }
        }
        .item-list{
            padding:0 .2rem;
            .item{
                height: .76rem;
                line-height: .76rem;
                
            }
            
            
        }
    }
}
</style>
