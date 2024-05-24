<template>
  <div class="character-card">
    <img :src="character.image" :alt="character.name" class="character-image" />
    <div class="character-info">
      <h2>{{ character.name }}</h2>
      <p><strong>Status:</strong> {{ character.status }}</p>
      <p><strong>Species:</strong> {{ character.species }}</p>
      <p><strong>Gender:</strong> {{ character.gender }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    character: Object,
  },
}
</script>

<style scoped>
.character-card {
  background: linear-gradient(145deg, #f0f0f0, #d4d4d4);
  border-radius: 20px;
  box-shadow: 5px 5px 15px rgba(0, 0, 0, 0.2),
    -5px -5px 15px rgba(255, 255, 255, 0.5);
  margin: 20px;
  overflow: hidden;
  display: flex;
  align-items: center;
  transition: transform 0.3s, box-shadow 0.3s;
  padding: 20px;
}

.character-card:hover {
  transform: translateY(-10px);
  box-shadow: 10px 10px 20px rgba(0, 0, 0, 0.3),
    -10px -10px 20px rgba(255, 255, 255, 0.6);
}

.character-image {
  width: 120px;
  height: 120px;
  object-fit: cover;
  border-radius: 50%;
  margin-right: 20px;
  border: 5px solid #fff;
}

.character-info {
  flex: 1;
}

.character-card h2 {
  margin-top: 0;
  font-size: 26px;
  color: #333;
  font-family: 'Permanent Marker', cursive;
}

.character-card p {
  margin: 8px 0;
  font-size: 16px;
  color: #666;
}

.character-card p strong {
  color: #333;
}
</style>
