<template>
  <div>
    <div class="song-list" v-if="songlist.length!=0">
      <div class="play" @click="play(0)">
        <span class="fa-play-circle-o ico"></span>
        <span class="text">播放全部</span>
        <span class="count">{{ totalCount }}</span>
      </div>
      <div class="list">
        <div v-for="(item,index) of songlist" :key="item.id" class="list-item" @click="play(index)">
          <div class="index" v-if="item.id!=$store.getters.playMusicID">{{ index+1 }}</div>
          <div class="index" v-else>
            <img style="height:25px" src="~@/components/common/loading/loading.gif" alt />
          </div>
          <div class="name">
            <p class="song-name">{{ item.name }}</p>
            <p class="singers">
              <span v-for="arlist of item.ar" :key="arlist.id">{{ arlist.name }}</span>
            </p>
          </div>
          <div class="operation">
            <span class="fa-ellipsis-v"></span>
          </div>
        </div>
      </div>
    </div>
    <loading v-show="$store.state.loadingShow" />
  </div>
</template>

<script lang='ts'>
import { loadingMixin, playMixin } from "@/utils/mixin";
import { Component, Vue, Prop } from "vue-property-decorator";
@Component({
  mixins: [loadingMixin, playMixin]
})
export default class SongList extends Vue {
  @Prop({
    default() {
      return [];
    }
  })
  songlist!: object[];

  get totalCount() {
    return `(共${this.songlist.length}首)`;
  }

  created() {}
}
</script>
<style scoped lang='less'>
.song-list {
  margin-top: -45px;
  background: white;
  border-radius: 15px 15px;
  .play {
    height: 50px;
    line-height: 50px;
    .ico {
      color: #4d4d4d;
      font-size: 25px;
      width: 50px;
      height: 50px;
      display: inline-block;
      text-align: center;
    }
    .text {
      font-size: 18px;
      height: 50px;
    }
    .count {
      color: #999;
    }
  }
  .list {
    .list-item {
      display: flex;
      height: 50px;
      align-items: center;
      text-align: center;
      .index {
        width: 50px;
        color: #999;
      }
      .name {
        flex: 1;
        text-align: left;
        overflow: hidden;
        .song-name {
          white-space: nowrap;
          overflow: hidden;
          text-overflow: ellipsis;
        }
        .singers {
          white-space: nowrap;
          overflow: hidden;
          text-overflow: ellipsis;
          span {
            color: #999;
            font-size: 12px;
          }
        }
      }
      .operation {
        width: 50px;
        span {
          color: #999;
        }
      }
    }
  }
}
</style>