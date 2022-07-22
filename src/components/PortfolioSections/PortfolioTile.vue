<template>
  <div class="col-lg-4 col-md-8 col-sm-10">
    <div class="single-blog">
    <!--A good first step is to do a single {{fields}} call and 
    make sure html displays-->
      <div v-if="fields.project_details.image" class="blog-header">
        <img
          class="img-fluid"
          loading="lazy"
          :src="fields.project_details.image"
        />
        <!-- Note above - could add alt text from butter -->
      </div>
        <div class="blog-body">
            <h5 class="package-name">
                {{ fields.project_details.name }}
            </h5>
            <!-- v-html removes escaping on data coming back from butter -->
            <div v-html="fields.project_details.description">
            </div>
        
            <ul>
                <li 
                    v-for="(technology, index) in fields.project_details.technologies" 
                    :key="index"
                > 
                    <strong>{{ technology.display_text }}</strong>
                </li>
            </ul>            
        </div>
            <div class="blog-footer">
                <a 
                    :href="fields.project_details.github_link" 
                    class="main-btn btn-hover"
                >
                    Get Source Code
                </a>
            </div>
        </div>
    </div>
</template>

<script setup>
defineProps([
  "fields",
]);
</script>

