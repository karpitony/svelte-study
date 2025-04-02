<script>
  let name = 'Svelte';
  let imageUrl = "https://github.com/sveltejs/branding/raw/master/svelte-logo.svg";
  let imageAlt = "Svelte logo";
  let href="https://svelte.dev";
  // let disabled = true;
  let attrs = {
    type: 'submit',
    disabled: false,
    class: 'btn'
  };
</script>

<p class="text">안녕 Svelte!</p>
<img src={imageUrl} alt={imageAlt}/>
<div>안녕하세요 {name}!</div>
<div>현재 시간은 {new Date()}입니다.</div>
<a {href}>Svelte 공식 홈페이지</a>

<button {...attrs}>전송</button>
<button type={attrs.type} disabled={attrs.disabled} class={attrs.class}>전송</button>

<!-- 주석 -->