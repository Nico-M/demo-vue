<template>
  <div class="work-info-list">
    <div class="list-header">
      <div class="header-item">序号</div>
      <div class="header-item">类型</div>
      <div class="header-item">数量</div>
    </div>
    <div class="list-content">
      <!-- 添加无限循环 -->
      <vue-seamless-scroll :data="workList" class="warp" :limitMoveNum="4">
        <ul class="item">
          <li v-for="item in workList" :key="item.id" class="list-row">
            <div class="list-item">{{ item.id }}</div>
            <div class="list-item">{{ item.type }}</div>
            <div class="list-item">{{ item.count }}</div>
          </li>
        </ul>
      </vue-seamless-scroll>
    </div>
  </div>
</template>

<script>
import vueSeamlessScroll from 'vue-seamless-scroll';

export default {
  name: 'WorkInfoList',
  components: {
    vueSeamlessScroll,
  },
  props: {
    workList: {
      type: Array,
      default: () => [
        { id: '01', type: '人数户数', count: 345 },
        { id: '02', type: '人均管理户数', count: 345 },
        { id: '03', type: '累计办理资金收入笔数金额', count: 345 },
        { id: '04', type: '资金支出笔数金额', count: 345 },
        { id: '05', type: '累计编制资金计划', count: 345 },
        { id: '06', type: '编制预算报表', count: 345 },
        { id: '07', type: '税务申报次数', count: 345 },
        { id: '08', type: '年度财务报表户数每户份数', count: 345 },
        { id: '09', type: '季度财务报表户数每户份数', count: 345 },
        { id: '10', type: '月度财务报表户数每户份数', count: 345 },
      ],
    },
  },
  data() {
    return {};
  },
};
</script>

<style lang="scss" scoped>
.work-info-list {
  width: 100%;
  background: rgba(0, 24, 64, 0.6);
  border-radius: 4px;

  .list-header {
    display: flex;
    padding: 12px 0;
    background: rgba(3, 43, 91, 0.8);
    color: #fff;
    font-weight: 500;

    .header-item {
      flex: 1;
      text-align: center;

      &:first-child {
        flex: 0 0 80px;
      }

      &:nth-child(2) {
        flex: 2;
      }

      &:last-child {
        flex: 0 0 100px;
      }
    }
  }

  .list-content {
    .list-row {
      display: flex;
      padding: 12px 0;
      color: #fff;
      border-bottom: 1px solid rgba(255, 255, 255, 0.1);

      &:hover {
        background: rgba(3, 43, 91, 0.4);
      }

      .list-item {
        flex: 1;
        text-align: center;

        &:first-child {
          flex: 0 0 80px;
        }

        &:nth-child(2) {
          flex: 2;
        }

        &:last-child {
          flex: 0 0 100px;
        }
      }

      // 添加条纹效果
      &:nth-child(2n) {
        background: #1e385f;
      }
    }
  }

  .warp{
    height: 400px;
    overflow: hidden;
    .item{
      padding:0;
      margin:0;
    }
  }
}
</style>
