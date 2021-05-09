<script lang="ts">
	let currId = 0
	let intervalms = 5000
	// 写真のファイル名リスト
	const images = [
		'/images/1.jpg',
		'/images/2.jpg',
		'/images/3.jpg',
		'/images/4.jpg',
		'/images/5.jpg',
	]

	const imgLen = images.length
	let positionLeft = 0

	const moveSlider = () => {
		positionLeft = currId * 100
	}

	const next = () => {
		currId = currId === imgLen-1 ? 0 : currId+1
		moveSlider()
	}

	const prev = () => {
		currId = currId === 0 ? imgLen-1 : currId-1
		moveSlider()
	}

	const getIndex = (index: number) => {
		currId = index
		moveSlider()
	}

	let interval = setInterval(next, intervalms)

	const autoPlay = () => {
		interval = setInterval(next, intervalms)
	}

	const stopPlay = () => {
		clearInterval(interval)
	}

</script>

<main>
	<div on:mouseover={stopPlay} on:mouseleave={autoPlay} class="container">
		<div class="slider" style="left: -{positionLeft}%;">
			{#each images as img, i}
				<img src={img} alt="猫画像その{i}" />
			{/each}
		</div> <!-- class="slider" -->
		<div class="arrow">
			<button on:click={prev} class="prev">Prev</button>
			<button on:click={next} class="next">Next</button>
		</div> <!-- class="arrow" -->
		<div class="pagination">
			{#each images as _, i}
				<button class={currId === i ? 'active' : ''}
					on:click={()=>getIndex(i)}
				/>
			{/each}
		</div> <!-- class="pagenation" -->
	</div> <!-- class="container" -->
</main>

<style>
  main {
    padding: 0px;
		margin: 0px;
    text-align: center;
		background-color: rgb(0,0,0);
	}

	/* 画像表示部分全体 */
  .container {
    position: relative;
    width: 100%;
		height: 100%;
    margin: 0 0;
    overflow: hidden;
		background-color: rgb(0,0,0);
		top:50%;
  }

	/* スライダー画像 */
  .slider {
    display: flex;
		justify-content: center;
		align-items: center;
    position: relative;
    transition: left 0.7s;
  }
  .slider img {
    width: 100%;
    height: auto;
    object-fit: cover;
    flex-shrink: 0;
  }

	/* 画像横のボタン部分 */
  .arrow {
    display: flex;
    justify-content: space-between;
    align-items: center;
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
  }
  .arrow button {
    margin-bottom: 0;
    padding: 12px;
    border: 0;
    background-color: rgba(255, 255, 255, 0.4);
    cursor: pointer;
  }

	/* 画像下のボタン */
  .pagination {
    position: absolute;
    bottom: 0;
    padding-bottom: 8px;
    width: 100%;
  }
  .pagination button {
    margin: 0 4px;
    width: 14px;
    height: 14px;
    border: 0;
    border-radius: 50%;
    background-color: rgba(200, 200, 200, 0.6);
    text-align: center;
    cursor: pointer;
  }
  .pagination .active {
    background-color: rgba(50, 120, 200, 0.7);
  }
</style>