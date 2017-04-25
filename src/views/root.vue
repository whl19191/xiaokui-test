<template>
  <div class="wrap">
    <h2>热电厂二期项目</h2>
    <b-form-input type="text" placeholder="搜索过滤建筑物名称" ></b-form-input>
    <b-card class="mb-2"
            title="Card title"
            sub-title="Card subtitle"
    >
    </b-card>
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
    }
</style>
