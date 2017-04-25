<template>
  <div class="wrap">
    <h2>热电厂二期项目</h2>
    <b-form-input type="text" placeholder="搜索过滤建筑物名称" ></b-form-input>
    <h4>单体建筑</h4>
    <div v-for="building in buildings">
      <b-card class="mb-2">
          <h5>{{ building.name }}</h5>
          <ul>
            <li>
              计划开始
              <p>{{ (building.start_date).slice(0,(building.start_date).indexOf('T')).split('-').join('')}}</p>
            </li>
            <li>
              计划完成
              <p>{{ (building.end_date).slice(0,(building.start_date).indexOf('T')).split('-').join('')}}</p>
            </li>
            <li>
              计划工期
              <p>{{ building.total_duration }}</p>

            </li>
            <li>
              已经施工
              <p>{{ building.total_elapsed }}</p>
            </li>
          </ul>
          <div class="progress-wrap">
              <p>实际进度</p>
              <div class="progress">
                  <div role="progressbar"  class="progress-bar progress-bar-striped progress-bar-animated" :style="'width:'+Math.round(building.real_progress * 100)+'%'">
                      <span>{{Math.round(building.real_progress * 100) + '%'}}</span>
                  </div>
                  <div role="progressbar"  class="progress-bar progress-bar-striped progress-bar-animated" :style="'width:'+Math.round(building.plan_progress * 100)+'%'" style="background:#333;">
                      <span style="top:1rem;color:#333;">{{Math.round(building.plan_progress * 100) + '%'}}</span>
                  </div>
              </div>
              <p>计划进度</p>
          </div>
      </b-card>
    </div>

    <div v-for="building in buildings">
      <h3>{{ building.name }}</h3>
      <ul>
        <li>计划开始: {{ building.start_date }}</li>
        <li>计划完成: {{ building.end_date }}</li>
        <li>计划工期: {{ building.total_duration }}</li>
        <li>已经施工: {{ building.total_elapsed }}</li>

        <li>下面两个做成进度条</li>
        <li>计划进度: {{ building.plan_progress }}</li>
        <li>实际进度: {{ building.real_progress }}</li>
      </ul>

      <h4>分布工程</h4>
      <ul>
        <li v-for="part in building.parts">
          <ul>
            <li>计划开始: {{ part.start_date }}</li>
            <li>计划完成: {{ part.end_date }}</li>
            <li>计划工期: {{ part.total_duration }}</li>
            <li>已经施工: {{ part.total_elapsed }}</li>

            <li>下面两个做成进度条</li>
            <li>计划进度: {{ part.plan_progress }}</li>
            <li>实际进度: {{ part.real_progress }}</li>
          </ul>
        </li>
      </ul>
      <hr>
    </div>
  </div>
</template>

<script>
export default {
  props: ['db'],
  data () {
    let buildings = this.db.buildings

    return {
      buildings: buildings
    }
  },
  computed: {
    progress () { return Math.round(this.building.plan_progress * 100) }
  }
}
</script>

<style lang="scss" rel="stylesheet/scss">
    .wrap{
        max-width:1000px;
        margin:0 auto;
        padding:5%;

        h2{
          line-height:3rem;
        }
        .form-control{
          border:none;
          background:#f8f8f8;
          line-height:3rem;
          font-size:17px;
          margin-bottom:1rem;
          &:focus{
            background:#f8f8f8;
          }
        }
        input::-webkit-input-placeholder {
          color:#bcbbbc;
        }
        h4{
          color:#c5c5c5;
          line-height:4rem;
        }
        .card{
          background: #f8f8f8;
          border:none;
          .card-block{
            padding:2rem;

            h5{
              text-align:center;
              line-height:3rem;
            }
            ul{
              display:flex;
              list-style:none;
              padding:0;
              justify-content:space-between;
              li{
                color:#a8a8a8;
                line-height:2rem;
                p{
                  color:#333;
                }
              }
            }
            p{
              line-height:3rem;
              margin-bottom:0;
              color:#a8a8a8;
            }
          }
        }
        .progress-wrap{
            .progress{
              background:#ecf0f1;
              position: relative;
              height:16px;
              overflow:visible;
              .progress-bar{
                background:#3498db;
                position: absolute;
                border-radius: .25rem;
                span{
                    position: absolute;
                    right:0;
                    top:-3rem;
                    line-height: 3rem;
                    font-size: 1rem;
                    color:#3498db;
                }
              }
            }
        }
    }
</style>
