<template>
  <div class="product-container container-fluid">
    <div class="row">
      <div class="col-md-5">
        <div class="product-img">
          <div class="carousel">
            <div class="carousel-inner">
              <div v-for="(image, index) in images" :key="index" :class="{ 'carousel-item': true, active: index === currentIndex }">
                <img :src="image.src" class="d-block w-100" alt="Slide {{ index }}">
              </div>
            </div>
            <a class="carousel-control-prev" @click="prevSlide" role="button">
              <span class="carousel-control-prev-icon" aria-hidden="false"></span>
              <link rel="stylesheet" class="dots" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@24,400,0,0" />
            </a>
            <a class="carousel-control-next" @click="nextSlide" role="button">
              <span class="carousel-control-next-icon" aria-hidden="false"></span>
              <link rel="stylesheet" class="dots" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@24,400,0,0" />
            </a>
          </div>
          <div class="carousel-thumbnails">
            <img v-for="(image, index) in images" :key="index" :src="image.src" class="thumbnail" :class="{ active: index === currentIndex }" @click="changeSlide(index)">
          </div>
        </div>
      </div>
      <div class="col-md-7">
          <h1><strong>Camiseta Premium - Preto</strong></h1>
            <div class="preco">
              <h3><strong>R$&nbsp;87,94</strong></h3>
            </div> 
        <table class="table">
            <thead>
              <tr>
                <th scope="col">Quantidade</th>
                <th scope="col">Desconto</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <th scope="row">2</th>
                <td>5% OFF</td>
              </tr>
              <tr>
                <th scope="row">3</th>
                <td>10% OFF</td>
              </tr>
              <tr>
                <th scope="row">4</th>
                <td>20% OFF</td>
              </tr>
            </tbody>
       </table>
        <div class="product-input">
          <p>Aplica-se a este produto e pode ser combinado com produtos de outras categorias selecionadas.</p>
          <span class="input-heading">Tamanho:</span>
          <select v-model="selectedMaterial" class="form-control">
            <option value="">P</option>
            <option value="tamanho">M</option>
            <option value="tamanho">G</option>
            <option value="tamanho">GG</option>
          </select>
          <span class="input-heading">Quantidade:</span>
          <input type="text" v-model.number="quantity" class="form-control small-textinput" placeholder="0">
          <h4 class="inventory" v-if="inventory > 0">Restam {{ this.inventory }} em estoque</h4>
          <h4 class="inventory" v-else>Sem estoque</h4>
          <button @click="addToCart" class="btn btn-primary bg-dark" style="margin: 5px;">Adicionar ao carrinho</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedMaterial: '',
      quantity: 0,
      inventory: 10,
      currentIndex: 0,
      images: [
        { src: 'https://brunxind.com/wp-content/uploads/2022/04/camiseta-basic-streetwear-preta1.jpg' },
        { src: 'https://brunxind.com/wp-content/uploads/2022/04/camiseta-basic-streetwear-preta3.jpg' },
        { src: 'https://brunxind.com/wp-content/uploads/2022/04/camiseta-basic-streetwear-preta5.jpg' },
        { src: 'https://brunxind.com/wp-content/uploads/2023/09/Camiseta-Streetwear-1.jpg' }
      ]
    };
  },
  methods: {
    addToCart() {
      if (this.quantity > 0 && this.inventory >= this.quantity) {
        console.log(` ${this.quantity} ${this.selectedMaterial} `);
        this.inventory -= this.quantity;
        this.quantity = 0;
      } else {
        alert('Quantidade não disponivel em estoque');
      }
    },
    nextSlide() {
      this.currentIndex = (this.currentIndex + 1) % this.images.length;
    },
    prevSlide() {
      this.currentIndex = (this.currentIndex - 1 + this.images.length) % this.images.length;
    },
    changeSlide(index) {
      this.currentIndex = index;
    }
  }
};
</script>

<style scoped>
.product-img img {
  width: 100%;
  height: auto;
  border: 1px solid #ccc;
}

.product-container {
  max-width: 1000px;
  margin: 20px auto;
}

.product-input {
  margin-bottom: 10px;
}

.input-heading {
  font-weight: bold;
  margin-top: 10px;
  display: block;
}

.small-textinput {
  height: 35px;
  width: 100%;
  max-width: 100px;
}

.inventory {
  color: green;
}
.product-container {
  margin-top: 60px;
}

.inventory {
  font-size: small;
}

.carousel {
  position: relative;
}
.carousel-inner {
  position: relative;
  width: 100%;
  height: 400px;

}
.carousel-item {
  display: none;
  transition: opacity 0.6s ease-in-out;
}
.carousel-item.active {
  display: block;
}
.carousel img {
  width: 100%;
  height: auto;
}
.carousel-control-prev,
.carousel-control-next {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  z-index: 1;
  cursor: pointer;
  
}
.carousel-control-prev {
  left: 0;
  color: black;
}
.carousel-control-next {
  right: 0;
  color: black;
}

.carousel-control-prev-icon{
  color: black;
}
.carousel-control-next, .dots{
  color: black;
}


.thumbnail {
  width: 50px;
  height: auto;
  cursor: pointer;
  margin-right: 5px;
  border: 1px solid #ccc;
}

.thumbnail.active {
  border-color: #007bff;
}

.carousel-thumbnails {
  margin-top: 10px;
  display: flex;
  justify-content: center;
  
}

.carousel-thumbnails img {
  width: 80px;
  height: 80px;
  cursor: pointer;
  margin-right: 5px;
  border: 1px solid #ccc;
  
}

.table{
  border: #f5f5ff;
}

.preco{
  color: #34E7F8;
}


</style>
