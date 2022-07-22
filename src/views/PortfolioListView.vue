<script setup>
import { butterCMS } from "@/utils/ButterCMS";
import { useApiError } from "@/utils/hooks";
import { useRoute } from "vue-router";
import { inject, nextTick, onMounted, ref, watch} from "vue";
import PortfolioTile from "@/components/PortfolioSections/PortfolioTile.vue";

// Second iteration - add Spinner
import Spinner from "@/components/Spinner.vue";

const { setError } = useApiError();
const portfolioProjects = ref(null);
const route = useRoute();
const {handleMounted} = inject("layout")

// Second iteration - Needed for Spinner.
const loading = ref(true)

// We're going to use onmounted here to allow us to extend later - e.g. spinner.
onMounted(async () => {
  try {
    // retrieve portfolio pages from butter
    // Note that if we wanted, we could order by field or other params.
    const pages = await butterCMS?.page.list("portfolio_page");
    portfolioProjects.value = pages?.data.data;
    await nextTick()
    // second iteration - flip loading value for spinner
    loading.value = false
    handleMounted()
  } catch (e) {
    setError(e);
  }
});
</script>
<template>
<!-- Spinner class-->
  <spinner v-if="loading"/>
<!-- spinner -->
  <section id="blog" class="blog-section">
    <div class="container">
      <div class="row justify-content-center">
        <div class="col-lg-6 col-md-10">
          <div class="section-title text-center">
            <h2>All Portfolio Projects</h2>
            <p>
              Check out my super awesome portfolio!
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