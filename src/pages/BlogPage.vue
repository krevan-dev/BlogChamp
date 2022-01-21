<template>
  <div class="card">
  <div class="card-body">
    <h5 class="card-title">{{activeBlog.title}}</h5>
    <p class="card-text">{{activeBlog.body}}</p>
    <p class="card-text"><small class="text-muted">Last updated 3 mins ago</small></p>
  </div>
  <img src="//placehold.it/300x300" class="card-img-bottom" alt="...">
</div>
</template>


<script>
import { computed } from '@vue/reactivity'
import { onMounted } from '@vue/runtime-core'
import { blogsService } from '../services/BlogsService'
import { AppState } from '../AppState'
import Pop from '../utils/Pop'
import { logger } from '../utils/Logger'
import { useRoute } from 'vue-router'
export default {
  setup(){
    const route = useRoute()
    onMounted(async () => {
      try {
        await blogsService.getBlogById(route.params.id)
      } catch (error) {
        Pop.toast(error.message)
        logger.log(error)
      }
    })
    return {
      activeBlog: computed(() => AppState.activeBlog)
    }
  }
}
</script>


<style lang="scss" scoped>

</style>