<template>
    <div class="card">
      <a :href="anime.url" target="_blank">
        <img :src="anime.images.jpg.large_image_url" :alt="anime.title" />
        <h3>{{ anime.title }}</h3>
      </a>
    </div>
  </template>
  
  <script>
  export default {
    props: ['anime'],
  };
  </script>
  
  <style lang="scss" scoped>
  .card {
    flex: 1 1 33%;
    width: 33%;
    max-width: 33%;
    padding: 0px 8px;
    margin-bottom: 16px;
  
    img {
      width: 100%;
      height: 500px;
      object-fit: cover;
      border-radius: 16px;
      box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.15);
      transition: 0.4s;
    }
    
    h3 {
      padding: 16px;
      color: #313131;
      transition: 0.4s;
    }
  
    &:hover {
      img {
        transform: scale(1.05);
      }
  
      h3 {
        color: #3d9dcd;
        transform: scale(1.05);
      }
    }
  }

  /* Media Queries */
  @media (max-width: 768px) {
    .card {
        flex: 1 1 50%;
        width: 50%;
        max-width: 50%;
    }
    
    img {
        height: 350px;
    }

    h3 {
        font-size: 16px;
      }
  }


@media (max-width: 480px) {
    .card {
    
    display: flex;
    
      flex: 1 1 100%;
      width: 100%;
      max-width: 100%;
      margin-bottom: 20px;
    }
  
    img {
      height: 250px;
    }
  
    h3 {
      font-size: 14px;
    }
  }
  
  </style>
  