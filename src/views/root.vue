<template>
  <div class="wrap">
    <h2>热电厂二期项目</h2>
    <b-form-input type="text" placeholder="搜索过滤建筑物名称" ></b-form-input>
    <h4>单体建筑</h4>
    <div v-for="building in buildings">
      <b-card>
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
          <div class="collapse-wrap">
              <div class="collapse-head">
                  <h5>显示分布工程进度</h5>
                  <span class="arr"></span>
              </div>
              <div class="collapse-con">
                  <h4>分布工程</h4>
                  <div v-for="part in building.parts">
                    <b-card class="mb-2">
                        <h5>{{ part.name }}</h5>
                        <ul>
                          <li>
                            计划开始
                            <p>{{ (part.start_date).slice(0,(part.start_date).indexOf('T')).split('-').join('')}}</p>
                          </li>
                          <li>
                            计划完成
                            <p>{{ (part.end_date).slice(0,(part.start_date).indexOf('T')).split('-').join('')}}</p>
                          </li>
                          <li>
                            计划工期
                            <p>{{ part.total_duration }}</p>

                          </li>
                          <li>
                            已经施工
                            <p>{{ part.total_elapsed }}</p>
                          </li>
                        </ul>
                        <div class="progress-wrap">
                            <p>实际进度</p>
                            <div class="progress">
                                <div role="progressbar"  class="progress-bar progress-bar-striped progress-bar-animated" :style="'width:'+Math.round(part.real_progress * 100)+'%'">
                                    <span v-if="part.real_progress">{{Math.round(part.real_progress * 100) + '%'}}</span>
                                </div>
                                <div role="progressbar"  class="progress-bar progress-bar-striped progress-bar-animated" :style="'width:'+Math.round(part.plan_progress * 100)+'%'" style="background:#333;">
                                    <span v-if="part.plan_progress" style="top:1rem;color:#333;">{{Math.round(part.plan_progress * 100) + '%'}}</span>
                                </div>
                            </div>
                            <p>计划进度</p>
                        </div>
                    </b-card>
                  </div>
            </div>
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
          margin-bottom: 2rem;
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
        .collapse-wrap{
            border-top:1px solid #e7e7e7;
            margin-top:1rem;
            width:106%;
            margin-left:-3%;
            margin-bottom: -2rem;
            .card{
                background: #fff;
            }
            .collapse-con{
                background: #fff;
                h4{
                    text-align: center;
                }
            }
            .collapse-head{
                position: relative;
                cursor: pointer;
                margin-bottom: 2rem;
                h5{
                    text-align: center;
                    font-size: 1rem;
                    color:#a7a7a7;
                }
                .arr{
                    background-image:url("data:image/svg+xml;charset=utf-8,%3Csvg%20xmlns%3D'http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg'%20viewBox%3D'0%200%2027%2044'%3E%3Cpath%20d%3D'M0%2C22L22%2C0l2.1%2C2.1L4.2%2C22l19.9%2C19.9L22%2C44L0%2C22L0%2C22L0%2C22z'%20fill%3D'%23bebebe'%2F%3E%3C%2Fsvg%3E");
                    background-repeat: no-repeat;
                    transform: rotate(-90deg);
                    position: absolute;
                    left:0;
                    right:0;
                    margin:0 auto;
                    width:1rem;
                    height:2rem;
                    bottom:-1.5rem;
                }
            }
        }
    }
</style>
