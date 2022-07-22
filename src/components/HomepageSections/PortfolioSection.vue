<template>
  <section id="portfolio" class="blog-section">
    <div class="container">
      <div class="row justify-content-center">
        <div class="col-lg-6 col-md-10">
          <div class="section-title text-center">
            <h2>Latest Portfolio Projects</h2>
            <p>
              A sample of my work
            </p>
            <p>
              <router-link class="main-btn btn-hover mt-5" to="/portfolio/">
                View All Portfolio Projects
              </router-link>
            </p>
          </div>
        </div>
      </div>
      <div class="row justify-content-center">
        <portfolio-tile
          v-for="(project, index) in portfolioProjects"
          :key="index"
          v-bind="project"
        />
      </div>
    </div>
  </section>
</template>

<script setup>
import PortfolioTile from "@/components/PortfolioSections/PortfolioTile.vue";
defineProps(["portfolioProjects"]);
</script>

<style scoped></style>
