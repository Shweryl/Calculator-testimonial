<template>
  <div class="container-fluid" :class="currentTheme">
    <div class="d-flex justify-content-center align-items-center vh-100">
      <div class="inner-wrap px-2">
        <div class="d-flex justify-content-between first-row align-items-center">
          <span class="fw-bold fs-1">calc</span>
          <div class="">
            <span class="fw-bold">THEME</span>
            <div class="toggle-wrap d-inline-block ms-3">
              <div class="d-flex justify-content-center">
                <div class="me-3 fw-bold">1</div>
                <div class="me-3 fw-bold">2</div>
                <div class="fw-bold">3</div>
              </div>
              <div class="radio-wrap rounded-pill">
                <input type="radio" class="me-2 form-check-input" :checked="currentTheme == 'theme1'? true : false" @click="switchTheme('theme1')">
                <input type="radio" class="me-2 form-check-input" :checked="currentTheme == 'theme2'? true : false" @click="switchTheme('theme2')">
                <input type="radio" class=" form-check-input" :checked="currentTheme == 'theme3'? true : false" @click="switchTheme('theme3')">
              </div>
            </div>
          </div>
        </div>
        <div class="row mt-2">
          <div class="col-12">
            <div class="result-box p-3 custom-border">
              <h2 class=" text-end mb-0 fw-bold">{{ outputTriggered || 0 }}</h2>
            </div>
          </div>
        </div>
        <div class="calculator-box custom-border mt-3 pt-0 p-3">
          <div class="row">
            <div class="col-3 g-3 text-center" v-for="input in inputs" :key="input">
              <button type="button" class="btn custom-btn custom-border fw-bold" :class="input == 'DEL' ? 'resetAndDelete' : ''" @click="calculate(input)">{{ input }}</button>
            </div>
          </div>
          <div class="row mt-3">
            <div class="col-6">
              <button type="button" class="btn w-100 resetAndDelete custom-border fw-bold" @click="reset">RESET</button>
            </div>
            <div class="col-6">
              <button type="button" class="btn bg-danger w-100 custom-border text-light fw-bold custom-font" @click="result">=</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>


export default {
  data(){
    return{
      inputs : [7,8,9,'DEL',4,5,6,'+',1,2,3,'-','.',0,'/','x'],
      currentValue : '',
      // operator : '',
      // preValue : '',
      outputTriggered : '',
      currentTheme : null
    }
  },
  methods : {
    // calculate(val){
    //   if(!isNaN(val) && !['+','-','/','x','DEL'].includes(val)){
    //     this.currentValue += val
    //     this.outputTriggered += val
    //   }
    //   if(val == 'x'){
    //     this.outputTriggered += val
    //     this.operator = '*'
    //     this.preValue = this.currentValue
    //     this.currentValue = ''
    //   }
    //   if(['+','-','/'].includes(val)){
    //     this.outputTriggered += val
    //     this.operator = val
    //     this.preValue = this.currentValue
    //     this.currentValue = ''
    //   }
    //   if(val == 'DEL'){
    //     this.outputTriggered = this.outputTriggered.slice(0,-1)
    //     if(this.currentValue){
    //       return this.currentValue = this.currentValue.substring(0,this.currentValue.length-1)
    //     }else if(this.operator){
    //       return this.operator = ''
    //     }else{
    //       return this.preValue = this.preValue.substring(0,this.preValue.length-1)
    //     }
        
    //   }
    // },
    // result(){
    //   this.outputTriggered = eval(this.preValue + this.operator + this.currentValue)
    //   this.outputTriggered = this.outputTriggered.toString()
    //   this.operator = ''
    //   this.preValue = ''
    //   this.currentValue = this.outputTriggered
    // }

    calculate(val){
      if(val != 'DEL'){
        this.outputTriggered += val
        if(val == 'x'){
          val = '*'
        }
        this.currentValue += val
      }else{
        this.outputTriggered = this.outputTriggered.slice(0,-1)
        this.currentValue = this.currentValue.slice(0,-1)
      }
      
    },

    result(){
      this.currentValue = eval(this.currentValue).toString()
      this.outputTriggered = this.currentValue
    },
    reset(){
      this.currentValue = ''
      this.outputTriggered = ''
    },
    switchTheme(theme){
      this.currentTheme = theme
    }
  },
  mounted(){
    this.switchTheme('theme1')
  }
}
</script>
<style lang="scss">
.theme1{
  background-color: var(--main-bg-color);

  .inner-wrap{
    width: 100%;
    max-width: 400px;

    .first-row{
      color: white;

      .radio-wrap{
        background-color: hsla(0, 0%, 0%,0.3);
        padding :  4px 8px 1px;

        .form-check-input{
          width : 13px!important;
          height : 13px!important;
          background-color: transparent!important;
          border-color: transparent!important;

          &:checked{
            background-color: rgb(219, 4, 4)!important;
            background-image: none!important;
          }
          &:focus{
            box-shadow: none!important;
          }
        }
      }
    }

    .result-box{
      background-color: black;
      color : white;
    }

    .custom-border{
      border-radius: 5px;
    }

    .calculator-box {
      background-color: rgba(0, 0, 0, 0.3);
      width: 100%;

      .custom-btn{
        background-color: white!important;
        color: var(--main-bg-color)!important;
        width: 100%;
        max-width : 70px;
        font-size : 20px!important;
      }

      .resetAndDelete{
        background-color: hsl(224, 26%, 45%)!important;
        color: white!important;
        font-size : 20px!important;
      }

      .custom-font{
        font-size : 20px!important;
      }
    
    }

    
  }
}


.theme2{
  background-color : #205b7a;

  .inner-wrap{
    width: 100%;
    max-width: 400px;

    .first-row{
      color: #a2bbcf;

      .radio-wrap{
        background-color: hsla(0, 0%, 0%,0.3);
        padding :  4px 8px 1px;

        .form-check-input{
          width : 13px!important;
          height : 13px!important;
          background-color: transparent!important;
          border-color: transparent!important;

          &:checked{
            background-color: yellow!important;
            background-image: none!important;
          }
          &:focus{
            box-shadow: none!important;
          }
        }
      }
    }

    .result-box{
      background-color: #a2bbcf;
      color : #142f44;
    }

    .custom-border{
      border-radius: 5px;
    }

    .calculator-box {
      background-color: rgba(0, 0, 0, 0.3);
      width: 100%;

      .custom-btn{
        background-color: #a2bbcf!important;
        color: #142f44!important;
        width: 100%;
        max-width : 70px;
        font-size : 20px!important;
      }

      .resetAndDelete{
        background-color: yellow!important;
        color: #142f44!important;
        font-size : 20px!important;
      }

      .custom-font{
        font-size : 20px!important;
      }
    
    }

    
  }
}

.theme3{
  background-color : #B7CE63;

  .inner-wrap{
    width: 100%;
    max-width: 400px;

    .first-row{
      color: #4B5842;

      .radio-wrap{
        background-color: hsla(0, 0%, 0%,0.5);
        padding :  4px 8px 1px;

        .form-check-input{
          width : 13px!important;
          height : 13px!important;
          background-color: transparent!important;
          border-color: transparent!important;

          &:checked{
            background-color: #B7CE63!important;
            background-image: none!important;
          }
          &:focus{
            box-shadow: none!important;
          }
        }
      }
    }

    .result-box{
      background-color: #4B5842;
      color : #DADDD8;
    }

    .custom-border{
      border-radius: 5px;
    }

    .calculator-box {
      background-color: rgba(0, 0, 0, 0.5);
      width: 100%;

      .custom-btn{
        background-color: #DADDD8!important;
        color: #8FB339!important;
        width: 100%;
        max-width : 70px;
        font-size : 20px!important;
      }

      .resetAndDelete{
        background-color: #B7CE63!important;
        color: #4B5842!important;
        font-size : 20px!important;
      }

      .custom-font{
        font-size : 20px!important;
      }
    
    }

    
  }
}









</style>

