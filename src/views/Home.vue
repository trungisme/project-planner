<template>
  <div class="home">
    <FilterNav @filterChange="filter = $event" :current="filter"/>
    <div v-if="filteredProjects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <Project :project="project" @delete="handleDelete" @complete="handleComplete"/>
      </div>
    </div>
  </div>
</template>

<script>
import Project from '@/components/Project.vue'
import FilterNav from '@/components/FilterNav.vue'
export default {
  name: 'Home',
  components: { Project, FilterNav },
  data() {
    return {
      projects: [],
      filter: 'all'
    }
  },
  computed: {
    filteredProjects() {
      if (this.filter === 'completed') {
        return this.projects.filter(project => project.complete)
      }
      if (this.filter === 'ongoing') {
        return this.projects.filter(project => !project.complete)
      }
      return this.projects
    }
  },
  mounted() {
    fetch('http://localhost:3000/projects')
      .then(res => res.json())
      .then(data => this.projects = data)
      .catch(err => console.log(err.message))
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter(project => project.id !== id)
    },
    handleComplete(id) {
      let p = this.projects.find(project => project.id === id)
      p.complete = !p.complete
    }
  }
}
</script>
