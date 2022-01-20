<template>
  <div class="container-fluid">
    <div class="row d-flex justify-content-center">
      <Blog v-for="b in blogs" :key="b.id" :blog="b"/>
    </div>
  </div>
</template>

<script>
import { computed, onMounted } from '@vue/runtime-core'
import { blogsService } from '../services/BlogsService'
import { AppState } from '../AppState';
export default {
  name: 'Home',
  setup() {
    onMounted(async () => {
      try {
        await blogsService.getBlogs();
      } catch (error) {
        Pop.toast(error.message, "error")
        logger.log(error)
      }
    });
    return {
      blogs: computed(() => AppState.blogs)
    }
  }
}
</script>

<style scoped lang="scss">
.home{
  display: grid;
  height: 80vh;
  place-content: center;
  text-align: center;
  user-select: none;
  .home-card{
    width: 50vw;
    > img{
      height: 200px;
      max-width: 200px;
      width: 100%;
      object-fit: contain;
      object-position: center;
    }
  }
}
</style>
