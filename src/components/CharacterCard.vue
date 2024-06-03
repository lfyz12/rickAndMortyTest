<template>
  <div class="character-card">
    <img :src="character.image" alt="character image" />
    <div class="card-info">
    <h1>{{ character.name }}</h1>
    <p class="status-info">{{ character.status }} <span>- {{ character.species }}</span></p>
    <p class="info-title">Last known location:</p>
      <p class="info-content">{{character.location.name}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CharacterCard',
  props: {
    character: Object
  }
}
</script>

<style scoped>
.character-card {
  width: 30vw;
  height: 220px;
  background: #313131;
  color: white;
  display: flex;
  margin-top: 2%;
}

.card-info {
  display: inline-block;
  margin-left: 2%;
}

.status-info {
  font-weight: bold;
  font-size: 20px;
}

.info-title {
  font-size: 16px;
  font-weight: 600;
  color: #919191;
}

.info-content {
  font-size: 22px;
  font-weight: 500;
}

img {
  width: 30%;
  height: 100%;
  object-fit: cover;
}
</style>
