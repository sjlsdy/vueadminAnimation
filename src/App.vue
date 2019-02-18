<template>
	<div id="app">
		<div class="list-frame">
			<div class="list-box">
				<div ref="abc123">abc123</div>
				<div class="list" @click="movediv(item.id)" v-for="item in waitData" :ref="'wait'+item.id">
					{{item.title}}
				</div>
			</div>
			<div class="list-box">
				<div class="list" v-for="item in doingData" :ref="'doing'+item.id">
					{{item.title}}
				</div>
				<div class="list" ref="nextdiv">D</div>
			</div>
		</div>
		<router-view/>
	</div>
</template>

<script>
	export default {
		name: 'App',
		data() {
			return {
				waitData: [{
					id: 3,
					title: '1C'
				}],
				doingData: [{
					id: 1,
					title: '1A'
				}, {
					id: 2,
					title: '1B'
				}, {
					id: 4,
					title: '1D'
				}],
			}
		},
		methods: {
			movediv(id) {
				this.doingData.push({
					id: 3,
					title: '1C'
				});
				setTimeout(() => {
					let startDiv = this.$refs['wait' + id][0];
					let overDiv = this.$refs['doing' + id][0];
					console.log(startDiv)
					console.log(this.$refs)
					let startLeft = startDiv.getBoundingClientRect().left;
					let startTop = startDiv.getBoundingClientRect().top;
					let overLeft = overDiv.getBoundingClientRect().left;
					let overTop = overDiv.getBoundingClientRect().top;
					let divwidth = overDiv.offsetWidth;
					console.log(divwidth)
					startDiv.style.width = divwidth + 'px';

					var move = document.styleSheets[0];
					move.deleteRule(6);
					move.insertRule("@keyframes mymove{0%{left:" + startLeft + "px;top:" + startTop + "px;} 100%{left:" + overLeft + "px;top:" + overTop + "px;}}", 6);
					console.log(move);

					startDiv.classList.add('move')
				})
			},
		}
	}
</script>

<style>
	#app {
		font-family: 'Avenir', Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		color: #2c3e50;
		margin-top: 60px;
	}
	
	.list-frame {
		width: 600px;
		height: auto;
		display: flex;
		border: #ccc 1px solid;
	}
	
	.list-box {
		flex: 1;
		background: #f9f9f9;
	}
	
	.list {
		height: 100px;
		border-bottom: #ccc 1px solid;
		background: #FFF;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	
	.move {
		position: fixed;
		animation: mymove 1s;
		animation-fill-mode: forwards;
	}
	
	@keyframes mymove {}
</style>