<script>
  let product = {
    name: 'Svelte Guide',
    price: 30000,
    id: 'svelte-book',
    images: [
      'https://github.com/developer-book/svelte-book/raw/main/static/svelte-book-1.png',
      'https://github.com/developer-book/svelte-book/raw/main/static/svelte-book-2.png',
      'https://github.com/developer-book/svelte-book/raw/main/static/svelte-book-3.png'
    ]
  };

  let sliderCenterIndex = 0;
  let sliderLeftIndex = product.images.length - 1;
  let sliderRightIndex = 1;

  function sliderMoveLeft() {
    const length = product.images.length;
    sliderCenterIndex = (sliderCenterIndex - 1 + length) % length;
    sliderLeftIndex = (sliderLeftIndex - 1 + length) % length;
    sliderRightIndex = (sliderRightIndex - 1 + length) % length;
  }

  function sliderMoveRight() {
    const length = product.images.length;
    sliderCenterIndex = (sliderCenterIndex + 1) % length;
    sliderLeftIndex = (sliderLeftIndex + 1) % length;
    sliderRightIndex = (sliderRightIndex + 1) % length;
  }

  let relatedProducts = [
    { name: 'React Book', price: 30000, id: 'react-book' },
    { name: 'Vue Book', price: 30000, id: 'vue-book' },
    { name: 'Angular Book', price: 30000, id: 'angular-book' },
  ];

  let cart = [];
  function addToCart(productId) {
    cart = [...cart, productId];
  }

</script>

<header class="header">
  <a class="header-title" href="/">Svelte Site</a>
  <nav>
    <ul class="header-links">
      <li>안녕하세요. 게스트님</li>
      <li>
        <a href="/cart">장바구니({cart.length})</a>
      </li>
    </ul>
  </nav>
</header>

<article class="product">
  <div class="product-main">
    <div class="image-container">
      <div class="slider">
        <img 
          src={product.images[sliderLeftIndex]}
          alt="sliderImage(left)"
          class="slider-item left"
        />
        <img 
          src={product.images[sliderCenterIndex]}
          alt="sliderImage(center)"
          class="slider-item center"
        />
        <img 
          src={product.images[sliderRightIndex]}
          alt="sliderImage(right)"
          class="slider-item right"
        />  
        <button class="slider-left-button" on:click={sliderMoveLeft}>←</button>
        <button class="slider-right-button" on:click={sliderMoveRight}>→</button>
      </div>
    </div>

    <div>
      <h2>{product.name}</h2>
      <dl>
        <dt>금액</dt>
        <dd>{product.price} 원</dd>
        <div>
          {#if !cart.includes(product.id)}
            <button on:click={() => addToCart(product.id)}>
              장바구니 담기
            </button>
          {:else}
            <button disabled>
              장바구니 담기 완료
            </button>
          {/if}
        </div>
      </dl>
    </div>
  </div>

  <footer>
    <h3>관련상품</h3>
    <ul>
      {#each relatedProducts as product}
        <li>
          <a href="/product/{product.id}">
            {product.name}
          </a>
        </li>
      {/each}
    </ul>
  </footer>
</article>

<style>
  :global(body) {
    font-family: Arial, sans-serif;
    background-color: #eee;
    margin: 0;
    padding: 0;
  }

  .header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 0 auto;
    background-color: #fff;
    padding: 0 15px;
    width: 100%;
    max-width: 800px;
    height: 50px;
  }

  .header-title {
    font-weight: bold;
  }

  .header-links {
    display: flex;
    gap: 10px;
    margin: 0;
    padding: 0;
    list-style: none;
  }

  .product {
    margin: 0 auto;
    background-color: #fff;
    padding: 15px;
    width: 100%;
    max-width: 800px;
  }

  .product-main {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
  }

  .image-container {
    width: 100%;
    max-width: 400px;
    overflow: hidden;
  }

  .image-container img {
    width: 100%;
  }

  .slider {
    position: relative;
    width: 80%;
    margin: 0 10%;
  }

  .slider-item {
    width: 100%;
    transition: transform 0.5s;
  }

  .slider-item.left {
    position: absolute;
    top: 0;
    right: 100%;
  }

  .slider-item.right {
    position: absolute;
    top: 0;
    left: 100%;
  }

  .slider-left-button {
    position: absolute;
    top: 50%;
    right: 100%;
  }

  .slider-right-button {
    position: absolute;
    top: 50%;
    left: 100%;
  }
</style>