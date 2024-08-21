<template>
    <div class="portfolio">
      <div v-if="loading" class="loading">Caricamento...</div>
      <div v-if="error" class="error">{{ error }}</div>
      <div v-if="projects.length > 0">
        <div class="project-card" v-for="project in projects" :key="project.id">
          <div class="project-image" :style="{ backgroundImage: `url(${project.image})` }"></div>
          <div class="project-content">
            <h3>{{ project.title }}</h3>
            <p>{{ project.description }}</p>
            <div class="project-links">
              <a :href="project.githubLink" target="_blank">GitHub</a>
              <a :href="project.demoLink" target="_blank">Live Demo</a>
            </div>
          </div>
        </div>
      </div>
      <div v-else-if="!loading && !error">Nessun progetto disponibile.</div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        projects: [],
        loading: true,
        error: null
      };
    },
    created() {
      this.fetchProjects();
    },
    methods: {
      async fetchProjects() {
        try {
          const response = await fetch('https://api.example.com/projects');
          if (!response.ok) {
            throw new Error('Errore durante il caricamento dei progetti');
          }
          const data = await response.json();
          this.projects = data.projects;  // Assicurati che l'API restituisca i dati in questo formato
        } catch (err) {
          this.error = err.message;
        } finally {
          this.loading = false;
        }
      }
    }
  }
  </script>
  
  <style lang="scss" scoped>
  
  $primary-color: #3498db;
  $secondary-color: #2c3e50;
  $background-color: #ecf0f1;
  $text-color: #333;
  $border-radius: 8px;
  $box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  
  body {
    font-family: 'Arial', sans-serif;
    background-color: $background-color;
    color: $text-color;
    margin: 0;
    padding: 20px;
  }
  
  .portfolio {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 20px;
    margin-top: 30px;
  }
  
  .project-card {
    background-color: white;
    border-radius: $border-radius;
    box-shadow: $box-shadow;
    overflow: hidden;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  
    &:hover {
      transform: translateY(-5px);
      box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
    }
  
    .project-image {
      width: 100%;
      height: 200px;
      background-size: cover;
      background-position: center;
    }
  
    .project-content {
      padding: 20px;
  
      h3 {
        margin-top: 0;
        margin-bottom: 10px;
        color: $primary-color;
        font-size: 1.5em;
      }
  
      p {
        margin-bottom: 15px;
        line-height: 1.5;
      }
  
      .project-links {
        display: flex;
        justify-content: space-between;
  
        a {
          text-decoration: none;
          color: $secondary-color;
          font-weight: bold;
          transition: color 0.3s ease;
  
          &:hover {
            color: $primary-color;
          }
        }
      }
    }
  }
  
  .loading {
    text-align: center;
    font-size: 1.2em;
    color: $secondary-color;
  }
  
  .error {
    text-align: center;
    color: red;
    font-size: 1.2em;
  }
  </style>
  