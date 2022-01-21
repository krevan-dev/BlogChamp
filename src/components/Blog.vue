<template>
  <div class="col-12">
    <div class="card mt-3 selectable" style="max-width: 98vw; min-height: 10vh;" @click="goToBlog()">
      <div class="row">
        <div class="col-md-2">
          <img :src="blog.imgUrl" class="img-fluid rounded-start" alt="">
        </div>
        <div class="col-md-10">
          <div class="card-body">
            <h5 class="card-title">{{blog.title}}</h5>
            <p class="card-text clip-text">{{blog.body}}</p>
            <div class="div d-flex justify-content-end align-items px-3">
                <p class="card-text"><small class="text-muted">{{blog.creator.name}}</small></p>
                <img :src="blog.creator.picture" class="img-fluid rounded-circle profile-icon ms-2" alt="">
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import { useRouter } from 'vue-router'
export default {
  props: {
    blog: {
      type: Object,
      required: true,
    },
  },
  setup(props){
    const router = useRouter();
    return {
      router,
      async goToBlog() {
        router.push({
          name: "BlogPage",
          params: {id: props.blog.id}
        })
      }
    }
  }
}
</script>


<style lang="scss" scoped>
.profile-icon {
  height: 2rem;
  width: 2rem;
}
</style>