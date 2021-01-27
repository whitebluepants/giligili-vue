<template>
  <div class="home">
    <div class=""> 
      <el-row :gutter="20">
        <el-col :span="4" v-for="video in videos" :key="video.id">
          <el-card class="video-card" @click.native="goVideo(video)">
            <img v-if="video.avatar" :src="video.avatar" class="video-avatar">
            <img v-else src="../assets/logo.jpg" class="video-avatar">
            <div>
              <div class="video-title">{{video.title}}</div>
              <div class="video-bottom">
                <span class="video-info" v-if="video.info">{{video.info.substring(0, 40)}}</span>
              </div>
            </div>
          </el-card>
        </el-col> 
      </el-row>
      <div class="block">
        <el-pagination
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
          :current-page="currentPage"
          :page-sizes="[6, 12]"
          :page-size="6"
          layout="total, sizes, prev, pager, next, jumper"
          :total="total">
        </el-pagination>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

import * as API from '@/api/video/';

export default {
  name: 'Home',
  data() {
    return {
      videos: [],
      total : 0,
      start: 0,
      limit: 6,
      currentPage: 0,
    };
  },
  methods: {
    handleSizeChange(val) {
      this.limit = val
      this.load()
    },
    handleCurrentChange(val) {
      this.start = this.limit * (val - 1)
      this.load()
    },
    load() {
      API.getVideos(this.start, this.limit).then((res) => {
        this.videos = res.data.items;
        this.total = res.data.total
      });
    },
    goVideo(video) {
      this.$router.push({ name: 'showVideo', params: { videoID: video.id} })
    }
  },
  components: {
  },
  beforeMount() {
    this.load();
  }
}
</script>


<style>
.video-avatar{
  width: 100%;
}
.video-title{
  margin: 4px 0px 5px 0px;
  text-overflow: ellipsis;
  white-space: nowrap;
  overflow: hidden;
}
.video-bottom{
  margin-top: 10px;
  text-overflow: ellipsis;
  white-space: nowrap;
  overflow: hidden;
}
.video-info {
  color: #909399;
}
.video-card {
  cursor: pointer;
  margin-bottom: 20px;
}
</style>