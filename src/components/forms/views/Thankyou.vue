<script>
export default {};
</script>
<template>
  <div>
    <img src="../../../assets/images/icon-thank-you.svg" alt="" />
    <h1>thank you !</h1>
    <p>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Quis autem et
      deleniti, exercitationem harum reprehenderit! Animi ullam aperiam cumque
      quaerat consequuntur pariatur, error tenetur iure harum eius ut eos
      quisquam repellat voluptates eligendi corporis eum soluta! Omnis nam ipsum
      dolorum!
    </p>
  </div>
</template>
<style scoped>
div {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  flex-direction: column;
  gap: 1rem;
}
h1 {
  font-size: 1.6rem;
  text-transform: capitalize;
  font-weight: bold;
  color: #1a2e4d;
}
p {
  width: 70%;
  text-align: center;
  color: #a1b2c2;
}

@media (max-width: 1280px) {
  div {
    background: white;
    width: 75%;
    margin: auto;
    height: 60vh;
    border-radius: 12px;
  }
}
</style>
