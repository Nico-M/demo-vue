<template>
  <div>
    <ChapterHeader title="排行榜" ></ChapterHeader>
    <div class="mt-8">
      <div class="ranking-list">
        <div class="ranking-header">
          <div class="header-item">排名</div>
          <div class="header-item">姓名</div>
          <div class="header-item">单据量</div>
        </div>
        <div class="ranking-content">
          <div v-for="(item, index) in rankList" :key="index" class="ranking-row">
            <div class="rank-icon">
              <img v-if="index < 3" :src="getRankIcon(index)" alt="rank" class="crown-icon" />
              <span v-else class="rank-number">{{ index + 1 }}</span>
            </div>
            <div class="name">{{ item.name }}</div>
            <div class="count">{{ item.count }}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import iconRate1 from '@/assets/images/bigScreen/icon-rate-1.png';
import iconRate2 from '@/assets/images/bigScreen/icon-rate-2.png';
import iconRate3 from '@/assets/images/bigScreen/icon-rate-3.png';
import ChapterHeader from './ChapterHeader.vue';

export default {
  name: 'RankingList',
  components: {
    ChapterHeader,
  },
  data() {
    return {
      rankList: [
        { name: '陈丽', count: 23414 },
        { name: '姜楠', count: 14321 },
        { name: '张莹', count: 12654 },
      ],
    };
  },
  methods: {
    getRankIcon(index) {
      const rankIcons = [iconRate1, iconRate2, iconRate3];
      return rankIcons[index];
    },
  },
};
</script>

<style lang="scss" scoped>
@import '../mixins.scss';
.ranking-list {
  width: 100%;
  background: rgba(0, 24, 64, 0.6);
  border-radius: 4px;
  font-family: 'puhuiti';

  .ranking-header {
    display: flex;
    padding: 12px 20px;
    background: rgba(3, 43, 91, 0.8);
    color: #fff;
    font-size: 16px;

    .header-item {
      &:nth-child(1) {
        flex: 0 0 80px;
      }
      &:nth-child(2) {
        flex: 1;
      }
      &:nth-child(3) {
        flex: 0 0 120px;
        text-align: right;
      }
    }
  }

  .ranking-content {
    .ranking-row {
      display: flex;
      align-items: center;
      padding: 0 20px;
      margin-top: 12px;
      color: #fff;
      height: 40px;
      // border-bottom: 1px solid rgba(255, 255, 255, 0.1);
      @include bg-image('@/assets/images/bigScreen/bg-rank-list');
      background-position: left center;
      background-size: cover;
      &:hover {
        background: rgba(3, 43, 91, 0.4);
      }

      .rank-icon {
        flex: 0 0 80px;

        .crown-icon {
          width: 30px;
          height: 30px;
        }

        .rank-number {
          font-size: 16px;
          color: #7ec7ff;
        }
      }

      .name {
        flex: 1;
        font-size: 16px;
      }

      .count {
        flex: 0 0 120px;
        text-align: right;
        font-size: 16px;
        color: #7ec7ff;
      }
    }
  }
}
</style>
