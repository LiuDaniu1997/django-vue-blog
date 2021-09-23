<template>

  <BlogHeader/>

  <!-- Header -->
  <header id="header" class="header">
    <div class="header-content">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            <h1 class="h1-large">Hi, I'm Kai,<br> Welcome to my Website</h1>
            <a class="btn-solid-lg" href="#introduction">Discover</a>
          </div> <!-- end of col -->
        </div> <!-- end of row -->
      </div> <!-- end of container -->
    </div> <!-- end of header-content -->

    <!-- Video Background -->
    <video autoplay loop muted id="video-background" poster="../assets/header-background.jpg" playsinline>
        <source src="../assets/header-background-video.mp4" type="video/mp4" />
    </video>
    <!-- end of video background -->

  </header> <!-- end of header -->
  <!-- end of header -->

  <BlogFooter/>

</template>

<script>
import BlogHeader from '@/components/BlogHeader.vue'
import BlogFooter from '@/components/BlogFooter.vue'


export default {
  name: 'Home',
  components: {BlogHeader, BlogFooter}
}
</script>

<style scoped>
/* Header */
.header {
	position: relative;
}

.header #video-background {
	position: absolute;
	right: 0;
	bottom: 0;
	min-width: 100%;
	min-height: 100%;
	width: auto;
	height: auto;
	z-index: -100;
}

.header .header-content {
	padding-top: 11rem;
	padding-bottom: 9rem;
	background: linear-gradient(rgba(21, 35, 63, 0.5), rgba(21, 35, 63, 0.5));
	background-size: cover;
	text-align: center;
}

.header .h1-large {
	margin-bottom: 2.25rem;
	color: #ffffff;
	font-size: 3rem;
	line-height: 3.75rem;
}

/* end of header */
</style>